# Math Study Coach · 数学长期学习教练

**让数学学习有衔接、有练习、有订正，也有可核对的学习记录。**

A Codex skill for ongoing math tutoring: resume from local records, learn in small steps, correct mistakes, and check progress with fresh questions.

[中文说明](#中文说明) · [English guide](#english-guide)

## 中文说明

### 这是什么

`math-study-coach` 是一套可安装到 Codex 的数学教学指令，默认用简体中文交流。它根据学习目录中的最新档案继续教学，适合数学补基础、高数学习和数学考试备考。

它关注“学生实际会了什么”：区分独立作答、提示后订正和教师示范，不把“听懂了”直接记为“已掌握”。具体目标、每天可用时间和教学偏好由你决定。

### 学习流程

**读取档案 → 接未答题或短复习 → 讲一个小点 → 等你作答 → 反馈与提示 → 订正 → 新题复测 → 保存进度**

- **衔接进度：** 保存最后的追问、已答部分和待补部分，从未完成题目和到期复习继续。
- **拆小讲解：** 没看懂就拆步骤；可以指定一道题或截图作为例子。
- **调整题量：** 熟悉内容可约 8 题一批，新内容通常先 2～3 题，订正可只问一个关键点。
- **理解日常输入：** 接受“平方、根号、乘”等表达，以及只补一个系数或缺项的回答；影响判断的歧义会先澄清。
- **保留真实证据：** 等你实际回答后再批改，记录提示和订正，不把教师写出的答案算作你的独立成果。
- **安排复习：** 根据表现安排新题和跨日复测；结束时保留未解决项和下一步。

### 安装

需要支持 skills 的 Codex，以及读取和写入学习目录的权限。下面的命令还需要 Git；也可使用 ZIP 安装。本技能本身没有额外的 Python 或 Node.js 依赖。

首次手动安装采用[当前官方文档](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills)列出的用户级目录：`~/.agents/skills/math-study-coach`。如果已经安装，请先看下方兼容说明，确认客户端实际识别的位置。

**Windows / PowerShell**

```powershell
$studyCoachSkills = Join-Path $env:USERPROFILE '.agents\skills'
New-Item -ItemType Directory -Path $studyCoachSkills -Force | Out-Null
git clone https://github.com/xwpwl/math-study-coach.git (Join-Path $studyCoachSkills 'math-study-coach')
```

**macOS / Linux**

```sh
study_coach_skills="$HOME/.agents/skills"
mkdir -p "$study_coach_skills"
git clone https://github.com/xwpwl/math-study-coach.git "$study_coach_skills/math-study-coach"
```

以上命令用于首次安装，目标文件夹应尚不存在。已有安装时先检查其中是否有自己的修改。

**不用 Git：** 在本仓库页面点击 **Code → Download ZIP**，解压后将包含 `SKILL.md` 的文件夹重命名为 `math-study-coach`，放入上述 `skills` 目录。确保路径直接是 `math-study-coach/SKILL.md`，不要多套一层文件夹。

安装后，在下一轮对话中调用技能；若未识别，重新打开 Codex 再试。

**安装兼容性**

- 官方主文档列出的用户级位置是 `~/.agents/skills`；[较早的官方教程](https://developers.openai.com/blog/eval-skills)仍使用 `~/.codex/skills`。
- 本次检查的 Windows Codex 桌面会话确实在可用技能清单中列出了 `~/.codex/skills/math-study-coach`；本机内置安装器说明也使用 `$CODEX_HOME/skills`。这只能证明本环境的识别情况，不能推广到所有客户端和版本。
- 客户端版本未能读取，记录为“未知”。macOS/Linux 安装尚未实机验证。检查日期：2026-10-20。
- 已安装时沿用客户端实际识别的目录，不要同时在两个目录放置同名技能。安装或更新后，确认技能选择器或可用技能清单能找到 `math-study-coach`，并核对加载文件的位置。

**更新已安装的技能**

GitHub 仓库更新不会自动更新本机安装副本。若安装目录本身是 Git 克隆，先检查本地修改，再在该目录执行 `git pull --ff-only`。若通过 ZIP 或文件复制安装，先备份自己的修改，再从最新仓库同步 `SKILL.md`、`references/records.md` 和 `agents/openai.yaml`。学习目录中的四份个人档案不属于安装更新文件。

### 使用方法

在 Codex 中打开一个专门的数学学习目录，例如 `数学学习`。**技能安装目录存放教学规则，学习目录存放你的个人档案。**

**1. 第一次开始**

在聊天框输入：

```text
$math-study-coach 我想开始长期数学学习。请先检查当前目录；
如果没有学习记录，就初始化档案并给我首次诊断题。
我的目标是补好基础并学习高数，每天能学数学 60 分钟。
```

目标和时间可按实际情况修改。无记录时，默认从三道基础诊断题开始，检查因式分解、解二次方程和代入检验。

**2. 下次继续**

回到同一个学习目录，输入：

```text
$math-study-coach 继续学习，先接上次未完成的题，再检查到期复习。
```

已有档案会被继续使用。换聊天时也应明确指定同一个学习目录。

**3. 学习过程中**

| 你想做什么 | 可以这样说 |
| --- | --- |
| 提交答案 | `1. (x+4)(x-3)；2. x的平方+2x；3. 不知道` |
| 只补一个地方 | `上一题第二项前面补一个 2，其余不变。` |
| 详细讲解 | `乘积法则和链式法则一起用没懂，用刚才那题一步一步讲。` |
| 增加题量 | `这些基础题可以多来几道，批量出题。` |
| 复习薄弱点 | `用新题检查商法则，先不要给答案。` |
| 结束学习 | `今天先到这里，保存进度，总结成果和下次安排。` |

### 学习档案

技能在获授权的学习目录中维护以下四个 Markdown 文件：

| 文件 | 内容 |
| --- | --- |
| `学习档案.md` | 学习目标、偏好、当前进度、最后追问及已答与待补部分 |
| `知识库.md` | 知识点、掌握状态、证据和复习安排 |
| `错题本.md` | 原始错误、提示订正及后续复测 |
| `学习日志.md` | 按时间记录的题目、真实作答和反馈 |

已有档案沿用原编号和引用关系；首次建档且尚无编号约定时，才默认使用 `MA` 前缀。针对同一道题的追问沿用原题号。

“已掌握”默认需要多个非重复新题及跨日表现支持；这是可调整的教学约定。某题答对可以继续推进，不必为了等状态升级而原地重复。

复习在你再次调用技能时处理，不会自动在后台提醒。技能默认只教数学；具体考试日期和大纲需要另行核实。仓库提供通用教学规则，不包含个人学习档案。

### 验证范围

安装路径的识别情况、格式校验和教学行为分别记录。跨上下文续学测试使用两个不继承父聊天历史的独立 Codex GPT 会话及合成档案，检查实际保存的四份文件。输入、快照和结果见[续学验证记录](tests/session-resume/REPORT.md)。该测试不等同于桌面界面重启或跨平台安装测试。

## English guide

### What it does

`math-study-coach` is a set of tutoring instructions for Codex. It uses local Markdown records to resume an ongoing math course, from foundational algebra to calculus and math exam preparation.

It tracks what the learner actually demonstrates, distinguishing independent answers, corrections made with hints, and tutor demonstrations. Goals, available study time, and teaching preferences come from the learner and their latest records.

**The default teaching language is Simplified Chinese.** To study in English, explicitly request English in your prompt. The four canonical record filenames remain in Chinese.

### Learning workflow

**Read records → Resume a question or review → Explain one concept → Wait for your answer → Give feedback and hints → Correct → Try fresh questions → Save progress**

- **Resume reliably:** Save the exact follow-up question, answered parts, and remaining parts to continue unfinished work and reviews due.
- **Explain in small steps:** Reuse a question or screenshot you provide and break down confusing steps.
- **Adjust the batch size:** Around eight familiar questions, two or three new or complex questions, or one correction at a time, depending on your preference.
- **Accept everyday notation:** Understand expressions such as “x squared,” Chinese math terms, and partial corrections; clarify ambiguities that affect grading.
- **Keep evidence accurate:** Do not count tutor-written answers as independent student work or treat “I understand” as proof of mastery.
- **Review over time:** Use fresh variations and later sessions to check retention, then save unfinished work and the next step.

### Installation

Use a Codex installation that supports skills, with permission to read and write your chosen study folder. Git is needed for the commands below; downloading a ZIP is also supported. The skill itself has no additional Python or Node.js dependencies.

For a new manual installation, use the user-level location in the [current official documentation](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills): `~/.agents/skills/math-study-coach`. For an existing installation, check the compatibility notes below before choosing a directory.

**Windows / PowerShell**

```powershell
$studyCoachSkills = Join-Path $env:USERPROFILE '.agents\skills'
New-Item -ItemType Directory -Path $studyCoachSkills -Force | Out-Null
git clone https://github.com/xwpwl/math-study-coach.git (Join-Path $studyCoachSkills 'math-study-coach')
```

**macOS / Linux**

```sh
study_coach_skills="$HOME/.agents/skills"
mkdir -p "$study_coach_skills"
git clone https://github.com/xwpwl/math-study-coach.git "$study_coach_skills/math-study-coach"
```

These commands are for a first installation; the destination folder should not already exist. Inspect an existing installation for your own changes before replacing it.

**Without Git:** Choose **Code → Download ZIP** on this repository page. Extract it, rename the folder containing `SKILL.md` to `math-study-coach`, and place it in your skills directory. The resulting path should be `math-study-coach/SKILL.md`, without an extra nested folder.

Invoke the skill on your next turn after installation. If Codex does not recognize it, reopen Codex and try again.

**Installation compatibility**

- The current official documentation lists `~/.agents/skills` for user-level skills; an [earlier official tutorial](https://developers.openai.com/blog/eval-skills) uses `~/.codex/skills`.
- The Windows Codex desktop session used for this check listed `~/.codex/skills/math-study-coach` among its available skills. Its bundled installer instructions also use `$CODEX_HOME/skills`. This is evidence about this environment, not a compatibility claim for every client and version.
- The client version could not be retrieved and is recorded as unknown. Installation on macOS/Linux has not been tested on those systems. Checked on 2026-10-20.
- Keep an existing installation in the directory your client recognizes. Avoid duplicate installations with the same skill name in both directories. After installing or updating, confirm that `math-study-coach` appears in the skill selector or available-skills list and check the loaded file location.

**Updating an installed copy**

Updating the GitHub repository does not automatically update your installed skill. If the installation directory is a Git clone, inspect local changes and then run `git pull --ff-only` inside that directory. For ZIP or copied installations, back up your customizations and sync `SKILL.md`, `references/records.md`, and `agents/openai.yaml` from the latest repository. The four personal records in your study folder are not installation files.

### How to use it

Open a dedicated math study folder in Codex. **The installed skill folder holds teaching rules; your study folder holds your personal learning records.**

**1. Start your first session**

Enter this in the chat:

```text
$math-study-coach Please teach me in English. Start an ongoing math course
in this folder. Check for existing records first; if none exist,
initialize the four study records and give me the initial diagnostic questions.
My goal is to build my algebra foundation and learn calculus.
I can spend 60 minutes a day on math.
```

Adjust the goal and time to your needs. With no existing records, the default diagnostic has three questions covering factorization, solving a quadratic by factoring, and checking a candidate root by substitution.

**2. Resume later**

Return to the same study folder and enter:

```text
$math-study-coach Continue in English from the latest records.
Resume unfinished questions first, then check reviews that are due.
```

Existing records are reused. When starting another chat, explicitly point it to the same study folder.

**3. During a session**

| Intent | Example message |
| --- | --- |
| Submit answers | `1. (x+4)(x-3); 2. x squared + 2x; 3. I don't know.` |
| Correct one part | `Add a coefficient of 2 to the second term of my previous answer.` |
| Ask for detail | `Explain how the product rule and chain rule work together, using that question step by step.` |
| Request more practice | `Give me a larger batch of these familiar questions.` |
| Review a weak area | `Check the quotient rule with fresh questions. Wait for my answers before showing solutions.` |
| Finish | `Stop here today. Save my progress and summarize what I learned and what comes next.` |

### Local learning records

The skill maintains four Markdown files in the authorized study folder:

| Filename | Purpose |
| --- | --- |
| `学习档案.md` | Learner goals, preferences, current progress, the latest follow-up question, and answered and remaining parts |
| `知识库.md` | Concepts, mastery status, supporting evidence, and review schedule |
| `错题本.md` | Original mistakes, corrections with hints, and later retests |
| `学习日志.md` | A chronological record of questions, actual answers, and feedback |

Existing records keep their identifiers and references. The `MA` prefix is only the default for a new set of records without an established numbering convention. Follow-up questions about the same problem retain its original question ID.

The default mastery check uses several distinct new questions and performance across study dates. It is an adjustable teaching convention. You can move on after sufficient successful practice while later review remains scheduled.

Reviews happen when you return to the skill; it does not send background reminders. It focuses on math. Official exam dates and syllabuses require separate verification. This repository contains reusable teaching rules, not personal study records.

### Validation scope

Installation discovery, format checks, and tutoring behavior are recorded separately. The context-handoff test uses two independent Codex GPT sessions without inherited parent-chat history and synthetic study records, then inspects the four files actually saved. See the [resume validation report](tests/session-resume/REPORT.md) for inputs, snapshots, and results. This is not a desktop UI restart test or a cross-platform installation test.

## 仓库结构 · Repository structure

```text
math-study-coach/
├── README.md                 # 中英文介绍与使用方法 / Bilingual guide
├── SKILL.md                  # 教学流程 / Tutoring instructions
├── agents/
│   └── openai.yaml           # 技能展示信息 / Skill display metadata
├── references/
│   └── records.md            # 档案和证据规则 / Record and evidence rules
└── tests/session-resume/     # 合成档案与行为验证 / Synthetic records and behavioral evidence
```

教学流程见 [SKILL.md](SKILL.md)，记录约定见 [references/records.md](references/records.md)。

See [SKILL.md](SKILL.md) for the tutoring instructions and [references/records.md](references/records.md) for the recordkeeping rules. Both instruction files are written in Chinese.
