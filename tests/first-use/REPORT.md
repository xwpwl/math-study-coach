# 首次使用验证记录 · First-use validation

**结果：本轮 3 个场景、6 个教学回合的目标行为检查通过。另有一项“真实档案在测试期间未变化”的独立检查未通过。** 这是两类不同检查的结果，不能将整个验证概括为全部通过。

所有学习者背景、题目和输出档案均为合成测试资料，不代表真实学生的活动或成绩。本目录整理的是已完成测试的证据，没有重新运行教学，也没有手工订正教学输出。

## 环境与范围

- 日期：2026-10-21，Asia/Shanghai。
- 规则基线：[1b71f383a79f6d4179edcda057b46f1194c432be](https://github.com/xwpwl/math-study-coach/tree/1b71f383a79f6d4179edcda057b46f1194c432be) 中的 `SKILL.md` 和 `references/records.md`。执行前已核对本机安装版与仓库版的 SHA-256 一致。
- Windows Codex 环境下三个独立 GPT 会话，以 `fork_turns=none` 启动，不继承父聊天历史，未覆盖模型。每组的第二轮继续在该组原会话中执行；精确模型版本和客户端版本未单独采集。
- 每组分配一个独立空学习目录，显式提供已安装技能路径和目录。会话被要求只读取技能、其引用规则及自身学习目录，只在自身目录写入学习数据，不读取真实档案、其他场景或评分标准。这是任务范围约束，不代表验证了操作系统层面的沙箱隔离。
- 首轮结束后先检查目录，再发送预先准备的第二轮输入。用户输入与检查项见 [test-plan.json](test-plan.json)；检查项没有发给执行教学的会话。
- 判定依据实际回复和保存的文件，不只依赖“已保存”的声明。A/B 各四份原始输出与本地冻结快照的哈希一致。
- 每组仅运行一次。该测试不验证桌面选择器自动发现、重启、无工作目录时的 UI、跨平台安装、并发写入恢复或长期可靠率；也没有验证学生后续答题后的策略调整。

## 公开证据的整理方式

`TEST_DIR_A`、`TEST_DIR_B`、`TEST_DIR_C` 分别代表三组隔离学习目录，`SKILL_DIR` 代表实际加载的技能安装目录。公开副本仅用这些占位符替换本机绝对路径；输入和实际回复放在代码块内展示，其余教学内容、数字、状态及措辞保留。

因此，公开快照不应与未替换路径的原始文件逐字节比较。目录清单里的 `Length` 是执行时原始文件的字节数，替换路径后的公开文件大小可能不同。重复的 `live` 文件不再收录；所有初始目录均为空，不需要初始档案模板。

真实学习档案内容、个人路径和真实档案的哈希对照不纳入仓库；保留相应检查的布尔结果及下方异常说明。[file-verification.json](file-verification.json) 中的 `SnapshotsMatch: true` 指原始输出与本地冻结快照一致，不表示公开副本与原始文件字节一致。

## 场景与结果

| 场景 | 首轮实际行为 | 第二轮实际行为 | 文件结果 |
| --- | --- | --- | --- |
| A：仅调用技能；随后同意建档，目标为购物折扣和单价，自述分数与百分数不熟，每天约 20 分钟 | 询问是否创建四份记录、学习目的和当前水平；未提前出题 | 使用折扣及单价两道购物题了解起点，保存应用目标和后续小点练习策略 | 首轮 0 项；同意后恰好四份记录 |
| B：仅调用技能；随后同意建档，已学极限和求导，希望理解积分累计量，每天约 40 分钟 | 询问建档、目的和水平；未提前出题 | 从流量乘时间、矩形面积与细分累加讲解，检查恒定累计量和左端矩形近似；未使用固定代数三题 | 首轮 0 项；同意后恰好四份记录 |
| C：已提供概率兴趣目标，但不清楚水平；随后拒绝建档 | 接受目标和“不清楚”，只问是否建档，未重复完整访谈 | 不建档，使用中奖比例和独立抽奖直觉题了解起点 | 两轮后均 0 项 |

A/B 的学习档案均记录学习目的、水平自述、时间预算、当前策略及依据；实际作答证据尚无，作答事件为 0。未因自述生成错题或升级为“已掌握”，未虚构学生回答，待答题没有数值答案。

## 输入、回复与文件证据

| 场景 | 输入与实际回复 | 目录检查 | 第二轮合成档案 |
| --- | --- | --- | --- |
| A | [第一轮](a_practical/turn-1.md)、[第二轮](a_practical/turn-2.md) | [第一轮](a_practical/after-turn-1.json)、[第二轮](a_practical/after-turn-2.json) | [学习档案](a_practical/after-turn-2/学习档案.md)、[知识库](a_practical/after-turn-2/知识库.md)、[错题本](a_practical/after-turn-2/错题本.md)、[学习日志](a_practical/after-turn-2/学习日志.md) |
| B | [第一轮](b_calculus/turn-1.md)、[第二轮](b_calculus/turn-2.md) | [第一轮](b_calculus/after-turn-1.json)、[第二轮](b_calculus/after-turn-2.json) | [学习档案](b_calculus/after-turn-2/学习档案.md)、[知识库](b_calculus/after-turn-2/知识库.md)、[错题本](b_calculus/after-turn-2/错题本.md)、[学习日志](b_calculus/after-turn-2/学习日志.md) |
| C | [第一轮](c_no_records/turn-1.md)、[第二轮](c_no_records/turn-2.md) | [第一轮](c_no_records/after-turn-1.json)、[第二轮](c_no_records/after-turn-2.json) | 无，用户拒绝建档 |

## 真实档案同期变化的检查

测试前后检查发现真实学习目录的四份文件哈希均有变化，因此 `RealRecordsUnchanged` 为 `false`。不能据此声称真实档案在测试期间保持不变，也未将这项检查改写成通过。

发现差异后，各会话复核了自身工具调用历史：A/B 的唯一写入命令通过显式设定隔离目录为 `workdir` 的 PowerShell 调用，使用 `Set-Content` 写入各自四份文件；未使用 `apply_patch` 或默认工作目录。C 只有读取技能和检查文件存在的命令，无写入。父会话只在测试目录保存测试证据。

这次调用历史复核未发现测试写入真实档案的操作，但没有追查同期变化的来源，也没有独立的文件系统写入追踪。因而不对变化来源作因果断言。没有覆盖或回滚真实档案。这项结果限制了对隔离性的结论，不改变三个场景的回复与隔离目录文件结果。

## 如何复测

1. 为 A/B/C 分别新建三个空目录，并使用要检验的技能版本。保留原始路径与技能文件哈希，避免使用个人学习目录。
2. 为每组启动独立、不继承其他聊天历史的 Codex 会话，提供该组目录、技能路径和工具范围约束；不提供评分标准或预期答案。
3. 发送 `test-plan.json` 中对应的 `turn1`。保存实际回复，检查目录是否仍为空，不能只看回复中的承诺。
4. 在该组原会话中发送对应的 `turn2`，保存回复和实际文件。若首轮行为偏离预期，保留该结果，不能改写模型输出使测试通过。
5. 核对建档授权、目标与水平是否已被考虑、教学起点是否匹配、待答状态与作答计数，以及 C 是否仍没有文件。分别报告教学行为检查和任何独立写入检查。

## 基线文件 SHA-256

- `SKILL.md`：`DE5E3F861156C8DD2CBD71B23D8213901A9C7E45300678F487AAB5CF861E55AE`
- `references/records.md`：`3173857B9B4A48BF6DACB985293D7F430B2A89E6D7603ACB6152D69668BC919B`

## English summary

**The target behavior checks passed in three synthetic scenarios, six tutoring turns in total. A separate check that real study files remained unchanged did not pass.** These results should not be summarized as an unconditional pass for the entire validation.

Three independent Codex GPT sessions started without inherited parent-chat history, each with an empty study folder. The second turn continued in the same session. No model override was supplied; exact model and client versions were not collected. The installed instructions matched commit `1b71f383a79f6d4179edcda057b46f1194c432be` before execution.

In A/B, invoking only the skill prompted questions about record creation, learning purpose, and current level; no files or exercises appeared before the reply. After consent, A used shopping discounts and unit prices, while B explained accumulated flow and area before two calculus-oriented exercises. Both created four records, kept self-assessment separate from verified performance, and recorded zero answer events. C reused a stated probability-interest goal, accepted uncertainty about level, and continued with probability questions after record creation was declined; its folder stayed empty.

The linked replies and snapshots retain the teaching output. Local paths are replaced with `TEST_DIR_A`, `TEST_DIR_B`, `TEST_DIR_C`, and `SKILL_DIR`, and reply Markdown is shown literally inside code blocks. File-list byte lengths refer to the original files, and `SnapshotsMatch` refers to the original local snapshots before path replacement. Real study contents and their hash comparisons are not published.

Real study files changed during the run. A follow-up review of the sessions' tool-call histories found only A/B writes inside their assigned folders and no writes from C, but the change source was not investigated and there was no independent filesystem write trace. No real files were reverted. This is a limit on the isolation conclusion, not evidence that the real files were unchanged.

Each scenario ran once. These checks cover explicit skill use with a known folder, not automatic discovery, UI restart, cross-platform installation, concurrent-write recovery, long-term reliability, or adaptation after subsequent student answers. To repeat, use three fresh folders, send each case's two inputs in order, preserve actual outputs, and inspect files as well as replies.
