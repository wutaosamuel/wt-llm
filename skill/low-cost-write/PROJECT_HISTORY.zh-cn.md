# 项目历史
<!-- 所有章节及其子内容均为可选。仅填写与本项目相关的部分,其余略去。
     本文件面向 AI 上下文而写。 -->

## 项目概述
- 项目类型:工具类(OpenCode AI 助手配置)。
- 目标:构建可复用的 OpenCode skills 与 commands,核心围绕一个成本优化工作流
  ——由高级模型生成内容,再由低成本模型逐字原样写入磁盘。

## 当前状态
- 在 `.opencode/` 下实现了两个产物:`low-cost-write` Skill 及配套的
  `low-cost-write` Command。
- 项目中已有 `update-history-memo` Skill 与 `init-history-memo` Command,作为
  风格/格式参照。

## 环境与工具链
- OpenCode,依赖 `@opencode-ai/plugin` 2.1.3(见 `.opencode/package.json`)。
- Windows / PowerShell 环境。

## 设计与关键决策
- 成本优化工作流:高级模型(Opus)生成内容,低成本模型(Haiku/Sonnet)负责写入,
  以降低成本。
- 模型分工依据:整文件逐字写入和短内容适合 Haiku;精确编辑、长内容、多文件/多步骤
  任务更适合 Sonnet,可靠性更高。
- 用户手动切换模型,因此约束机制被设计为指令形式(Skill + Command),而非自动路由。
- 同时创建 Skill(靠 description 自动加载)与 Command(通过 `/low-cost-write`
  手动调用),使同一套规则覆盖自动与手动两种触发路径。
- 命名统一为 `low-cost-write`。
- 采用内容分隔符约定(`<<<CONTENT>>>...<<<END>>>`),让执行模型把被包裹的文本
  严格当作数据,绝不当作指令执行。

## 踩坑与经验教训
- 使用低成本模型执行写入,最大的隐性成本不是 token,而是内容被悄悄篡改导致的高级
  模型返工。缓解措施:硬性铁律(逐字照抄、禁止改写)加上强制的读回校验。
- 系统提示曾报告"没有可用的 skills",但实际项目是支持 skills 的(发现了已存在的
  skills 目录)。教训:应核实真实项目环境,而非轻信外围系统提示。
- Command 不应设计成"进入模式后等待用户另行粘贴内容"。当内容已由高级模型在同一
  session 中生成时,应主动回看 session 提取内容与目标路径,而非围绕 `$ARGUMENTS`
  空等;否则无参数调用 `/low-cost-write` 时会无内容可写、只能停在等待态。
- Command/Skill 文件正文用中文还是英文,只影响文件本身内容,不影响当前 session 的
  交流语言。选用英文纯粹是沿用现有约定,并非为了规避语言影响。
- 写入时若目标文件已存在,Write 工具要求先 Read 一次才允许覆盖(即便文件为空)。
  低成本执行器流程应把"写前先读"纳入固定步骤,避免首次写入被拦下。

## 开发历史
| 日期 | 摘要 |
|------|------|
| 2026-07-06 | 设计了低成本逐字写入工作流(高级模型生成、低成本模型写入)。创建了 `low-cost-write` Skill(`.opencode/skills/low-cost-write/SKILL.md`)与 Command(`.opencode/commands/low-cost-write.md`),二者均强制逐字照抄、禁止改写、仅操作单一文件、并要求强制读回校验,采用 `<<<CONTENT>>>...<<<END>>>` 分隔符约定。初始化了本项目历史备忘。 |
| 2026-07-06 | 修复 `/low-cost-write` 只"进入等待模式"却不执行的问题。Command 与 SKILL 原设计全程围绕 `$ARGUMENTS` 并教模型等待用户另行粘贴内容,导致无参数调用时无内容可写。改为:默认从当前 session 回看、提取高级模型最近生成的最终内容及其指明的目标路径并逐字写入;路径不明确则停下询问、绝不猜测;`Path/Operation/<<<CONTENT>>>` 手动格式降级为可选备用。 |
| 2026-07-06 | 实测了新的 `/low-cost-write` 工作流:进入低成本执行器模式后从本 session 提取高级模型已生成的内容,写入 `tmp.txt`,写后读回校验通过;随后经字节级复核确认 75 字节、LF 行尾、零差异,验证通过。 |
| 2026-07-06 | 细化 `low-cost-write` 的目标路径解析:文件名+工作目录能唯一确定文件时直接写、不再询问,仅在真正歧义(多处同名/无法推断目录)时才停下问;减少了繁琐确认。 |

## 下一步
- (已完成)已在 `tmp.txt` 上验证 `low-cost-write` 工作流并通过字节级读回校验。
  后续可再补一个"内容被故意改动"的负向用例,确认读回校验能主动报告差异。
- 明确尾随换行约定:内容末尾是否保留换行需由交付内容决定,执行器逐字保留、不自行增删。
- 考虑本项目是否需要一个 `AGENTS.md`。

## 约定与规范
- Skill/Command 文件使用英文内容(沿用现有约定;文件语言不影响 session 交流语言),
  frontmatter 遵循现有 `update-history-memo` 风格(`name`、`description`、
  `license: MIT`、`compatibility: opencode`、`metadata`)。
- `/low-cost-write` 默认从当前 session 提取高级模型已生成的内容并写入其指明的目标
  文件;目标路径不明确时停下询问、绝不猜测。手动 `Path/Operation/<<<CONTENT>>>`
  格式为可选备用。
