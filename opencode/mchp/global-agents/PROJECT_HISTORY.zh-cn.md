# 项目历史

## 项目概述
- 该文件夹（`opencode/mchp/global-agents`）用于存放面向 OpenCode 的全局
  `AGENTS.md` 规则文件，主要针对 Microchip MCU 开发场景（MPLAB X IDE 及
  MPLAB X 的 VS Code 插件）。
- 项目类型：工具配置 / AI 助手配置类。

## 设计与关键决策
- `AGENTS.md` 的顶层大标题为 `# WorkStation rules`，方便未来在同级追加其他
  工具/开发环境的规则章节（`##` 子标题），无需重构文件结构。
- MPLAB X 项目检测规则：当前工作目录本身以 `.X` 结尾，或当前工作目录下存在
  以 `.X` 结尾的子文件夹时，视为处于 MPLAB X 项目环境中。
- `mcc_generated_files` 的保护范围：仅限于 `.X` 项目根目录下直属的
  `mcc_generated_files` 文件夹（不匹配任意深度的同名目录），但该目录下所有
  层级的文件都受此规则保护。
- 执行机制：在编辑/新建/删除 `mcc_generated_files/` 下任何文件之前，助手必须
  每次都向用户询问确认，不允许因同一会话中曾获批准而跳过后续确认，因为 MCC
  重新生成代码时会覆盖手动修改。
- 内容语言：按用户要求使用纯英文撰写（该文件主要供大模型读取，而非终端用户）。

## 开发历史
| 日期 | 摘要 |
|------|------|
| 2026-08-19 | 在 `opencode/mchp/global-agents` 下创建 `AGENTS.md`，顶层大标题为 `WorkStation rules`，内含 MPLAB X 项目检测规则及保护 `mcc_generated_files` 目录（修改前必须每次确认）的规则。 |

## 下一步
- 后续可在 `WorkStation rules` 下继续添加其他 Microchip 工具/开发环境相关的
  规则子章节（例如其他 IDE、构建系统等）。

## 其他
- 本文件位于 `opencode/mchp/global-agents` 目录下，与仓库根目录（如有）的历史
  记录文件相互独立，专门记录该规则文件夹的演进历史。
