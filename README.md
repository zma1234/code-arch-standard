# Java 分层架构编码规范（Qoder Plugin）

## 插件简介

本插件为 Java 项目提供**五层分层架构编码规范**指导，涵盖：

- 五层架构：Controller → 混合业务层 → 单领域业务层 → 数据访问层（Repo）→ Mapper
- 各层命名规则（如 `IT*Service`、`IT*Repo`、`IT*Mapper`）
- 各层职责划分与依赖约束（严禁越层依赖）
- 编码注意事项（判空工具类使用、分页查询规范等）

## 来源说明（Provenance）

- **内容来源**：`D:\project\itelHomeNv\itelHomeNv-common\copilot-instructions.md`（项目仓库根目录的编码指令文件，分支 `feature/v1.0.0`）
- **来源仓库**：https://git.transsion.com/itel/server/itelHomeNv/itelHomeNv-common.git
- **Logo**：插件内置生成的 SVG（五层堆叠图形），非来源于外部资源

## 包含内容

| 文件 | 说明 |
|------|------|
| `.qoder-plugin/plugin.json` | 插件清单 |
| `skills/code-arch-standard/SKILL.md` | 分层架构规范技能（完整保留源文件全部规范条款） |
| `assets/avatar.svg` | 插件图标 |

## 省略说明

- 源文件无 `references/`、`scripts/` 等附属文件，无需复制
- 源文件末尾的空行与排版噪声已清理，规范条款内容未做删减

## 安装与使用

1. 将本插件目录 `code-arch-standard` 复制到 Qoder 插件目录，或通过 Qoder 插件安装入口导入
2. 在项目中进行开发、评审或重构时，Agent 会根据技能描述自动匹配并应用该规范
3. 也可手动调用技能：`/code-arch-standard`

## 设置说明

无需外部凭据、MCP 服务或环境变量。

## 验证记录

- 离线校验器验证结果见最终交付摘要（Output Summary）
