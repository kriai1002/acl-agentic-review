# ACL Agentic Review

严格、公正、可追溯的 ACL / EMNLP / NAACL / ARR 模拟审稿 skill。

An evidence-grounded NLP peer-review skill for Codex. It checks each consequential criticism against the paper's strongest counterevidence before assigning scores and writing a simulated meta review. Chinese output is the default; ask for English when needed.

## 它做什么

- 阅读论文正文、图表、公式、结果、局限性与可访问附录。
- 按“主张—证据—反证—严重程度”复核主要问题，撤回已被论文回答的批评。
- 分别评价 Soundness、Excitement、Overall Assessment、Confidence 与复现等维度。
- 输出完整审稿报告、修改优先级、评分表和 Simulated Meta Review。
- 支持新版本重审、rebuttal 后更新，以及“直接给分”等简短追问。

采用原提示词的**模拟 5 分制**：3.5 为主会边缘，4.0 为明确 Accept，4.5 为 Strong Accept，5.0 留给极少数突出贡献。它不是会议官方评分尺度，不能直接换算录取概率。

## 安装到 Codex

### 方式一：让 skill-installer 从 GitHub 安装

在 Codex 中发送：

```text
使用 skill-installer，从 https://github.com/kriai1002/acl-agentic-review 安装 skills/acl-agentic-review。
```

### 方式二：下载 ZIP 并复制

1. 在 GitHub 点击 **Code → Download ZIP**，解压。
2. 将 `skills/acl-agentic-review` 整个文件夹复制到以下位置：

   - Windows：`%USERPROFILE%\.codex\skills\acl-agentic-review`
   - macOS / Linux：`~/.codex/skills/acl-agentic-review`
   - 已设置 `CODEX_HOME` 时：`$CODEX_HOME/skills/acl-agentic-review`

3. 打开新会话；若未出现该 skill，重启 Codex。

注意复制的是包含 `SKILL.md` 的内层目录。正确结构：

```text
~/.codex/skills/acl-agentic-review/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── report-format.md
    └── scoring-rubric.md
```

如果该目录已经存在，先备份本地修改，再更新文件。

## 使用

上传或提供能够访问的论文 PDF 后发送：

```text
$acl-agentic-review 按 ACL 主会标准完整审阅这篇论文。
```

指定会议信息有助于篇幅检查：

```text
$acl-agentic-review 目标是 ACL 2027 长文，按中文输出完整审稿。
请核查当年的官方要求；不能核实的篇幅项标为 Cannot Verify。
```

重审与简短追问：

```text
$acl-agentic-review 这是修订稿和 rebuttal。沿用上次的问题编号，说明哪些问题已解决，再更新评分。
```

```text
基于刚才的审稿，Overall Assessment 多少分？直接给出分数和推荐类别。
```

英文输出：

```text
$acl-agentic-review Review the attached paper in English and provide the full report, scores, and a simulated meta review.
```

## 报告包含什么

1. 阅读范围与篇幅、领域、研究完整性、审稿操纵检查。
2. Summary。
3. Strengths。
4. Weaknesses / Major Concerns。
5. 主张—证据—反证—严重程度复核。
6. 已核实的 Missing References / Related Work。
7. 修改建议、必要修复与可选增强、升分和降分条件。
8. 各维度详细评价。
9. Score Summary。
10. 六个直接判断。
11. Simulated Meta Review。

用户要求局部或简短回答时，skill 会尊重请求，不强制输出完整模板。

## 能力与边界

- 这个项目提供可复用的评审指令，不包含模型、审稿数据集或自动跑实验的服务。
- 不需要专用 API key；PDF 读取、联网核查和模型能力由运行环境提供。
- 无法访问的材料会单独说明；不会把它们自动当作论文缺陷。
- 引用和会议规则需要实际核查；离线环境会标注核查限制。
- “Agentic”指主动取证和反向复核，不代表已经获得多个独立 reviewer 的意见。
- 模拟评审不能替代会议实际评审，不提供经过统计校准的录取概率。

## 项目结构

```text
acl-agentic-review/
├── README.md
├── LICENSE
└── skills/
    └── acl-agentic-review/
        ├── SKILL.md
        ├── agents/openai.yaml
        └── references/
            ├── report-format.md
            └── scoring-rubric.md
```

基于作者提供的中文《ACL Agentic Review — 高标准模拟审稿 Prompt》整理，去除重复段落并拆分为工作流程、报告结构和评分尺度。项目不附带具体投稿论文、审稿实例或私人路径。

MIT License，允许下载、使用、修改和再分发，保留许可证即可。本项目与 ACL、EMNLP、NAACL、ARR 或 OpenAI 无隶属或背书关系。
