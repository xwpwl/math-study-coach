# 数学长期学习教练

一个用于 Codex 的数学学习 skill。它读取当前学习目录中的最新档案，衔接未答题与复习，按小点讲解、真实作答、最小提示、订正和新题复测的流程推进。

## 功能

- 接受“平方、根号、乘”等中文数学表达和局部补答。
- 区分用户实际作答、提示后订正与教师示范，保留真实学习证据。
- 按难度调整题量，维护学习档案、知识库、错题本和学习日志。
- 根据最新档案续学，不把固定题号或某一天的进度写入 skill。

## 安装

将整个仓库目录放到 Codex 的 skills 目录下，文件夹名为 `math-study-coach`。如果设置了 `CODEX_HOME`，使用其中的 `skills` 目录；否则使用 `~/.codex/skills`。

目标目录尚不存在时，可执行：

```sh
git clone https://github.com/xwpwl/math-study-coach.git ~/.codex/skills/math-study-coach
```

仓库为私有时，需要使用有访问权限的 GitHub 账号。

## 使用

在已获授权的数学学习目录中开启聊天，输入：

```text
$math-study-coach 继续学习
```

已有记录时提供或保留 `学习档案.md`、`知识库.md`、`错题本.md`、`学习日志.md`。没有记录时，明确要求开始长期数学学习并初始化档案，skill 会从诊断开始。具体考试目标、时间安排和当前进度以用户要求及档案为准。

## 文件结构

- `SKILL.md`：教学流程。
- `references/records.md`：档案与证据规则。
- `agents/openai.yaml`：技能名称与默认调用提示。
