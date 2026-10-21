# 已有档案与部分缺档续学验证

日期：2026-10-21（Asia/Shanghai）
仓库基线：`fe8905b73e7eb0c8c3438bf9c74beca61c5e1b4c`；技能规则与安装版逐字节一致，哈希见 [skill-baseline.json](skill-baseline.json)。

**结论：四组、八个教学回合均没有重复询问已有学习目的与水平，没有清空或回退原有题目进度。发现一处跨日补建主档后的会话汇总表述不一致，不能将所有记录检查概括为完全通过。**

## 方法与证据

- A/B/C 是预先设计的三组场景；D 在发现 C 会话计数变化后追加，作为同日对照。每组执行一次，两轮在该组同一会话内继续。
- 四组均为不继承父聊天历史的独立 Codex GPT 会话（`fork_turns=none`），未覆盖模型，精确模型版本和客户端版本未单独采集。另有独立只读会话复核文件。
- 执行会话只获准读取当前安装版 skill、其引用规则和自身 live 目录，并仅在自身目录写学习数据；未提供评分标准、预期输出或其他组结果。写入要求使用明确的隔离路径，不依赖默认工作目录。
- initial 为测试组织者预设的合成资料，包含学习目的、水平自述、实际练习证据、当前待订正题与编号。所有背景、历史作答和进度均为测试输入，不代表真实学生。
- A 初始四份文件齐全；B 只有学习档案与日志；C/D 没有学习档案，目标、水平和进度可从其余记录恢复。
- 逐轮保留实际回复、文件快照、哈希比较和差异。未手工修正输出；initial 哈希前后不变，最终快照与各自 live 文件一致。
- 本轮仅操作合成测试目录，没有读取真实学生四份档案进行教学或制作测试素材。任务范围约束不等于验证了操作系统沙箱隔离。
- 输入和检查项见 [test-plan.json](test-plan.json)，结构与历史保留核验见 [verification.json](verification.json)，初始文件哈希见 [initial-hashes.json](initial-hashes.json)。独立复核摘要见 [review-note.md](review-note.md)。
- 这是显式提供技能路径、已知工作目录和合成资料的单次行为测试；不验证桌面自动加载、一般可靠率、全部缺档组合或损坏文件恢复。

## 统一初始进度

- 目的：为大学微积分课程补齐求导基础，学习乘积与链式法则组合；每天约 30 分钟，偏好拆步。
- ALG-Q001 已独立正确回答并说明幂函数求导规则，知识点 ALG-K001 为“初步会”；复习日期 2026-10-23。
- ALG-Q002：对 f(x)=(x+1)√(2x+3) 求导，x>-3/2。原答两项写全，但第二项漏了内层导数因子；错题 ALG-E001“订正中”。
- 最后追问：“先只看根号里面，(2x+3)' 等于多少？”尚未收到回答。
- 初始共 2 道题、2 次作答、1 条错题、1 次会话；前缀 ALG，下一作答 ALG-A003，下一题 ALG-Q003，已有会话 ALG-S001。
- A/B/C 的初始学习日期是 2026-10-20；D 仅把 C 初始资料中的该日期替换为 2026-10-21，其余内容相同。复习日期仍为 2026-10-23。

## 实际结果

| 场景 | 第一轮 | 第二轮 | 结果 |
| --- | --- | --- | --- |
| A：档案齐全 | 直接接内层导数追问，无建档询问或重复背景访谈；只追加续学记录 | 用户答“2”，要求只批改该步；正确记为局部补答 ALG-A003，完整订正仍待完成 | 正确衔接。只增加 1 次真实作答，题目/错题/会话计数不变 |
| B：缺知识库、错题本 | 读出已有进度，询问是否补建这两份；未创建或修改文件 | 同意后从原档案和日志恢复知识点、错题及复习日期，继续原追问 | 只新增缺失文件；已有档案/日志追加续学说明，原编号和计数保留 |
| C：缺主学习档案，跨日 | 从知识库、错题本、日志读出进度，询问是否补建主档；未创建或修改文件 | 同意后恢复目标、水平、题目与作答编号；知识库和错题本字节不变；会话改为 ALG-S002 | 学习进度保留，但旧“当前记录汇总”与新会话计数不一致，详见下节 |
| D：缺主学习档案，同日对照 | 同样只询问是否补建，未创建或修改文件 | 补建后继续原题并沿用 ALG-S001；知识库和错题本字节不变 | 目标、水平、编号和计数均保留 |

A 中原始历史作答与正确证据保留，仅更新当前补答状态和作答计数；不把教师提示后的数字补答算成整题独立完成。B/C/D 中补建同意均没有被记成数学作答，也没有分配新题。所有组都保留 2026-10-23 的复习安排。

“保留进度”不表示所有文件必须字节不变：正常学习可以增量更新当前状态、计数或追加日志。本次检查的是原有事实、未完成项和历史证据没有被清空或回退。

## C 的会话汇总问题与限制

C 的 [新学习档案](c_missing_profile/after-turn-2/学习档案.md)及[日志末尾](c_missing_profile/after-turn-2/学习日志.md)将会话计为 2 次、当前 ALG-S002、下一 ALG-S003；同一日志较早的“当前记录汇总”仍写着 1 次、下一 ALG-S002，没有明确把这块改标为历史快照。因此文件内存在两个容易被当成当前值的计数口径。

不能仅凭该变化断定“补建主档错误重置进度”：原记录日期与测试日期不同，当前规则未明确规定跨日是否应建立新学习会话；新会话划分有可能合理。题目、原答、未完成部分和复习并未丢失。

追加的 D 同日对照沿用了 ALG-S001，但每个场景只运行一次，不能据此证明日期是差异的唯一原因。可确认的改进点是：明确跨日会话划分依据，并让旧“当前汇总”更新或标记为历史，避免恢复时误读。当前只记录发现，没有修改技能或修正测试输出。

## 输入、回复和逐轮文件

| 场景 | 实际交互 | 快照与哈希比较 |
| --- | --- | --- |
| A | [第一轮](a_complete/turn-1.md)、[第二轮](a_complete/turn-2.md) | [初始主档](a_complete/initial/学习档案.md)、[第一轮](a_complete/after-turn-1.json)、[第二轮](a_complete/after-turn-2.json)、[最终主档](a_complete/after-turn-2/学习档案.md)、[最终日志](a_complete/after-turn-2/学习日志.md) |
| B | [第一轮](b_missing_support/turn-1.md)、[第二轮](b_missing_support/turn-2.md) | [初始主档](b_missing_support/initial/学习档案.md)、[第一轮](b_missing_support/after-turn-1.json)、[第二轮](b_missing_support/after-turn-2.json)、[补建知识库](b_missing_support/after-turn-2/知识库.md)、[补建错题本](b_missing_support/after-turn-2/错题本.md) |
| C | [第一轮](c_missing_profile/turn-1.md)、[第二轮](c_missing_profile/turn-2.md) | [初始日志](c_missing_profile/initial/学习日志.md)、[第一轮](c_missing_profile/after-turn-1.json)、[第二轮](c_missing_profile/after-turn-2.json)、[补建主档](c_missing_profile/after-turn-2/学习档案.md)、[日志差异](c_missing_profile/after-turn-2-diffs/学习日志.md.diff) |
| D | [第一轮](d_missing_profile_same_day/turn-1.md)、[第二轮](d_missing_profile_same_day/turn-2.md) | [初始日志](d_missing_profile_same_day/initial/学习日志.md)、[第一轮](d_missing_profile_same_day/after-turn-1.json)、[第二轮](d_missing_profile_same_day/after-turn-2.json)、[补建主档](d_missing_profile_same_day/after-turn-2/学习档案.md)、[日志差异](d_missing_profile_same_day/after-turn-2-diffs/学习日志.md.diff) |

各目录还保留完整 initial、after-turn-1、after-turn-2 和相应差异。复测时将某组 initial 复制到新目录，按 test-plan 的输入顺序执行；保留所有真实输出，不能为了符合预期手工改写。

本轮没有修改 skill，也没有提交或推送仓库。
