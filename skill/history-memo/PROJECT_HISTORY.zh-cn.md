# 项目历史

<!-- 本文件是供 AI 阅读的开发项目上下文（软件 / 硬件 / 嵌入式 / 工具开发 / 混合）。
     所有章节及其子内容均为「可选」——只填写与本项目相关的内容，其余省略。
     不要编造内容。
     请与 PROJECT_HISTORY.en.md 保持同步。 -->

## 项目简介
- 工具开发项目：一套 OpenCode/Claude「历史备忘」系统，用于跨 session 记录供
  AI 阅读的项目上下文。
- 交付物：一个手动调用的 skill（`update-history-memo`）、一个初始化命令
  （`/init-history-memo`）、以及中英双语上下文模板
  （`PROJECT_HISTORY.en.md` / `.zh-cn.md`）。
- 适用范围：通用开发项目——软件、硬件、嵌入式、工具开发及混合。

## 当前状态
- Skill、命令、两个模板文件均已创建并可用。
- 模板文件位于 `template/` 目录；当前活跃的上下文文件位于项目根目录。

## 设计与关键决策
- 按项目性质拆分为两个独立 skill；本仓库只实现开发项目 skill（通用项目 skill 暂缓）。
- 双语上下文文件以后缀区分（`.en` / `.zh-cn`）；两者必须一一对应保持同步。
- 手动调用（不自动触发）；每次写入前必须先经人工审核。
- session 回顾不使用 git；不自动修改 `AGENTS.md`（仅给建议）。
- 所有模板章节均为可选——只填相关内容，绝不编造。
- 增设末尾 `Others`/「其他」兜底章节，避免无处归类但有用的信息丢失；约束其保持
  简短、不当垃圾堆。

## 避坑指南
- OpenCode 不会自动加载 `PROJECT_HISTORY.*.md`（只自动读 `AGENTS.md`）。若想把它
  用作 session 上下文，需在 `AGENTS.md` 里加一行，指示 AI 在 session 开始时读取
  `PROJECT_HISTORY.en.md`。
- 此处 shell 为 Windows PowerShell 5.1：不支持 `&&`，`ls -la` 会报错。应使用
  `Get-ChildItem`；日期用 `Get-Date -Format "yyyy-MM-dd"`。

## 关键参考与数据手册
- OpenCode Skills 文档：https://opencode.ai/docs/skills/
- OpenCode Commands 文档：https://opencode.ai/docs/commands/

## 待解决问题
- 可能再编写一个面向通用（非开发）项目的独立 skill。

## 开发历史

| 日期 | 摘要 |
|------|------|
| 2026-07-02 | 创建了 `update-history-memo` skill、`/init-history-memo` 命令，以及中英双语 `PROJECT_HISTORY` 模板。范围定为通用开发（软件 / 硬件 / 嵌入式 / 工具开发）。加入 PowerShell+bash 双日期命令、「只记录成功方案」规则，并将硬件 tips 精简为只记录理由。项目类型标签改为 `hardware`。 |
| 2026-07-02 | 在两个模板、两个根目录上下文文件、skill 和命令中新增 `Others`/「其他」兜底章节（附「不当垃圾堆」约束）。 |

## 下一步计划
- 可选：在 `AGENTS.md` 加入那一行，使备忘每次 session 自动加载。
- 可能再编写一个面向通用（非开发）项目的独立 skill。

## 约定与规范
- Skill 文件 `SKILL.md` 用英文写；上下文文件双语。
- Skill 名 / 命令名采用小写连字符形式：`update-history-memo`、`init-history-memo`。

## 其他
<!-- 不属于以上任何章节、但可能有用的信息。
     保持简短；不要当成垃圾堆。一旦某条明确归属某章节，就移到那个章节去。 -->
