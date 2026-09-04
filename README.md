# 代码分层架构编码规范（Qoder Plugin）

## 插件简介

本插件为项目提供**分层架构编码规范**指导，当前包含 Java 规范（Python 规范待补充），涵盖：

- 分层架构：Controller → 混合业务层 → 单领域业务层 → 数据访问层（Repo）→ Mapper
- 各层命名规则（如 `IT*Service`、`IT*Repo`、`IT*Mapper`）
- 各层职责划分与依赖约束（严禁越层依赖）
- 编码注意事项（判空工具类使用、分页查询规范等）

## 包含内容

| 文件 | 说明 |
|------|------|
| `.qoder-plugin/plugin.json` | 插件清单 |
| `rules/java.md` | Java 分层架构编码规范（完整规范条款） |
| `rules/python.md` | Python 规范占位文件（内容待补充） |
| `assets/avatar.svg` | 插件图标（五层堆叠图形，插件内置生成） |

## 来源说明（Provenance）

- **Logo**：插件内置生成的 SVG，非来源于外部资源
- 源文件无 `references/`、`scripts/` 等附属文件，无需复制；排版噪声已清理，规范条款内容未做删减

## 安装与使用

1. 将本插件目录 `code-arch-standard` 复制到 Qoder 插件目录，或通过 Qoder 插件安装入口导入
2. 本插件为 rules-only 插件，不含可通过斜杠命令调用的技能；在进行开发、评审或重构时，Agent 会根据规则描述自动匹配并注入对应规范

## 设置说明

无需外部凭据、MCP 服务或环境变量。

## 仓库地址

- https://github.com/zma1234/code-arch-standard.git

## 验证记录

- 已通过 Qoder 官方离线校验器（`validate_qoder_plugin.py`）校验：`ok: true`
- 唯一提示为 "plugin.json does not declare skills"，属 rules-only 插件的正常状态
