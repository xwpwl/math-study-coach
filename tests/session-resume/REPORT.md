# 续学验证记录 · Context-handoff validation

**结果：本次单场景测试通过。** 结论来自两轮实际保存的四份文件及对应回复，不只依据回复中的“已保存”。

所有档案都是合成测试资料，不代表真实学生的活动或成绩。初始档案由测试组织者设置；`after-a` 与 `after-b` 是各轮执行后保存的文件快照，没有手工订正测试输出。

## 环境与范围

- 日期：2026-10-20，Asia/Shanghai。
- 技能规则基线：[349ccbacd778a6d69ea208c88dc5e4c0cc7ca24b](https://github.com/xwpwl/math-study-coach/tree/349ccbacd778a6d69ea208c88dc5e4c0cc7ca24b) 中的 `SKILL.md` 和 `references/records.md`。
- 执行环境：Windows Codex 桌面环境中的两个独立 GPT 测试会话，均不继承父聊天历史（`fork_turns=none`），未指定模型覆盖。精确模型版本标识未单独采集。
- 两个会话只能读取安装版技能、其记录规则和同一隔离学习目录中的四份文件；只能修改这四份文件，不读取真实学习档案、另一会话的聊天、快照目录或评分标准。
- 测试前已将安装版两份规则文件与上述发布版逐字节核对一致。
- 第一轮完成并冻结快照后才启动第二轮。第二轮通过共享的四份学习文件获得上下文，没有收到第一轮的聊天记录。
- 本机父会话的技能清单列出了 `~/.codex/skills/math-study-coach`；测试会话明确获得该技能路径。因此本测试验证显式使用技能后的记录与恢复行为，不证明其他客户端的自动发现行为。
- 客户端版本未知。未执行桌面 UI 重启测试、macOS/Linux 安装测试，也未测试断电或并发写入恢复。

## 初始设置

初始四份文件已经存在，沿用 `ALG` 前缀。只有一道待答题 `ALG-Q001`，所属学习会话是 `ALG-S001`，尚无作答或错题记录。

题目：求 `f(x)=(x+1)√(2x+3)` 的导数，`x>-3/2`。

知识库包含乘积法则和根式链式求导的一般公式，没有本题完整参考答案。教学偏好为：遇到不会的步骤，先问一个关键小问题。

## 会话 A

以下为传入的用户请求；“当前目录”由测试环境指定为隔离学习目录。

```text
$math-study-coach 继续当前目录的学习。我的答案是：根号(2x+3)+(x+1)/(2根号(2x+3))。第二项这里不太会，你先只问我一个关键小问题，不要直接给完整答案。
```

实际最终回复：

```text
你把乘积法则的两项都写出来了，第一项也正确。第二项先检查根号内层的导数。

**先只看根号里面：\((2x+3)'\) 等于多少？**

已保存本次作答和待补步骤。
```

文件检查确认：首次作答被记录为 `ALG-A001`，错题为 `ALG-E001`；学习档案和日志保存了实际追问及提示，题目仍未完成。

## 会话 B

此会话以空的父聊天历史启动，只通过技能和四份文件继续学习。传入的用户请求：

```text
$math-study-coach 我换个聊天接着刚才的学习，目录就是上面指定的目录。我的回答是：2。先只批改我这一处回答，不讲完整解答，也不出新题。
```

实际最终回复：

```text
对，\((2x+3)'=2\)，这一步答对了。

已保存这次局部补答；第二项的完整订正留待后续继续。
```

文件检查确认：本次回答记录为 `ALG-A002`，对应同一道题的内层导数追问；原追问已答，第二项完整订正仍待完成。

## 检查结果

| 检查项 | 实际结果 |
| --- | --- |
| 保存能恢复的具体追问 | A 的学习档案与日志均记录 `(2x+3)' 等于多少`，以及已答、待补部分 |
| 保留原编号 | 两轮均沿用 `ALG` 前缀，未将旧记录改成 `MA` |
| 简短补答对应正确 | B 将原答“2”解释为 `(2x+3)'=2`，没有当作整题导数 |
| 题目与会话不重复计数 | 最终仍为 1 道题、1 次学习会话，题号和会话号均沿用原值 |
| 作答事件计数正确 | 从 0 次到 1 次再到 2 次；新增 `ALG-A002`，下一个编号为 `ALG-A003` |
| 错题不重复建立 | 最终仍为 `ALG-E001` 一条错题，追加了局部补答，状态仍为“订正中” |
| 不虚增整题完成或掌握程度 | 第二项及整题仍未完成；链式求导仍为“学习中”，没有记为独立完成新题 |
| 保留真实帮助和历史证据 | 原错误答案、A 的提示与追问、B 的原答均保留；B 标注为提示后局部补答 |
| 遵守当轮范围 | B 没有给完整解答、出新题或追加追问，并记录原追问已经答对 |
| 四份文件一致 | 档案、日志、知识库和错题本对局部答对、完整订正未完成的描述一致 |

## 文件快照

| 文件 | 初始输入 | 会话 A 后 | 会话 B 后 |
| --- | --- | --- | --- |
| 学习档案 | [initial](initial/学习档案.md) | [after-a](after-a/学习档案.md) | [after-b](after-b/学习档案.md) |
| 知识库 | [initial](initial/知识库.md) | [after-a](after-a/知识库.md) | [after-b](after-b/知识库.md) |
| 错题本 | [initial](initial/错题本.md) | [after-a](after-a/错题本.md) | [after-b](after-b/错题本.md) |
| 学习日志 | [initial](initial/学习日志.md) | [after-a](after-a/学习日志.md) | [after-b](after-b/学习日志.md) |

日志中旧事件的状态描述保留当时事实；当前状态以最新事件和学习档案为准。

## 如何复测

1. 将 `initial` 下四份文件复制到新的隔离学习目录，使用要检验的技能版本。
2. 在不继承旧聊天的会话中发送 A 的请求，等它完成保存，冻结四份文件。
3. 另开一个不继承旧聊天的会话，仅提供技能路径、学习目录和 B 的请求。
4. 检查实际四份文件，逐项核对上表；不要用“老师说已保存”代替文件检查，也不要把手工修正后的文件当成模型输出。

这里的 B 输入针对本次实际追问设计。如果复测中 A 问了另一件事，应保留原输出并据实评价，不能强行把“2”判成正确。

## English summary

**This single synthetic scenario passed.** Two independent Codex GPT sessions used the same isolated study files without inheriting the parent conversation. Session A saved its actual follow-up question. Session B received only the student response `2` and the shared files, correctly matched it to the inner derivative, and recorded a partial correction.

Inspection covered all four saved files. The original `ALG` identifiers were preserved. Final counts were one question, two answer events, one error entry, and one study session. The full derivative remained unfinished, and mastery was not inflated. The raw initial records and unedited output snapshots are linked above.

The tested instructions are from commit `349ccbacd778a6d69ea208c88dc5e4c0cc7ca24b`. The installed copy was verified to match before execution. Both sessions used the current Codex GPT configuration without a model override; the exact model version was not separately captured.

The Windows parent session listed the skill under `~/.codex/skills`; the test sessions were explicitly given that path. The client version could not be retrieved. This is evidence of file-based context handoff in one controlled run, not a desktop UI restart test, an automatic-discovery test on other clients, a cross-platform installation test, or a general reliability score.

To repeat the test, copy the initial files to a fresh folder, run A, preserve its files, and start a separate session with B and those files only. Inspect the saved records against the table. If A asks a different question, report that outcome honestly rather than forcing the numeric response to fit.
