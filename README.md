# 代码分层架构编码规范（Qoder Plugin）

## 插件简介

本插件为项目提供**分层架构编码规范**指导，当前包含 Java 规范（Python 规范待补充），涵盖：

java：
- 分层架构：Controller → 混合业务层 → 单领域业务层 → 数据访问层（Repo）→ Mapper
- 各层命名规则（如 `IT*Service`、`IT*Repo`、`IT*Mapper`）
- 各层职责划分与依赖约束（严禁越层依赖）
- 编码注意事项（判空工具类使用、分页查询规范等）

## 包含内容

| 文件 | 说明 |
|------|------|
| `.qoder-plugin/plugin.json` | 插件清单 |
| `rules/java.md` | Java 分层架构编码规范（完整规范条款） |
| `rules/python.md` | Python 分层架构编码规范（基础框架，条款待完善） |
| `assets/avatar.svg` | 插件图标（五层堆叠图形，插件内置生成） |
- 源文件无 `references/`、`scripts/` 等附属文件，无需复制；排版噪声已清理，规范条款内容未做删减

## 来源说明（Provenance）

- **Logo**：插件内置生成的 SVG，非来源于外部资源

## 安装与使用

### 安装步骤

**方式一：手动复制目录（推荐）**

1. 克隆或下载本仓库到本地
2. 将 `code-arch-standard` 目录复制到 Qoder CN 用户插件目录：
   - Windows：`C:\Users\<用户名>\.qoder-cn\plugins\custom\`
   - macOS / Linux：`~/.qoder-cn/plugins/custom/`
3. 确认目录结构完整：

   ```text
   code-arch-standard/
   ├── .qoder-plugin/plugin.json   # 插件清单
   ├── rules/java.md               # Java 分层架构编码规范
   ├── rules/python.md             # Python 分层架构编码规范
   └── assets/avatar.svg           # 插件图标
   ```

4. 重启 IDE（或重新打开项目）使插件生效

**方式二：通过插件管理界面导入**

1. 打开 IDEA 设置：`Settings → Qoder CN → 个人设置 → 插件`
2. 点击右上角 **导入 ZIP**（本地 zip 包）或 **新建插件**
3. 导入完成后，在「自定义」列表确认出现 **代码分层架构编码规范**（范围：用户），并勾选「启用」
4. 重启 IDE

### 验证安装

按以下路径进入规则页，确认插件携带的规则已加载：

> Qoder CN 智能会话面板（右侧边栏图标）→ 面板右上角用户头像 ▾ → 个人设置 → 找到 **规则** 分组 → 点击进入**规则页**

（也可通过 IDEA `Settings → Other Settings → Qoder CN → 个人设置 → 规则管理` 进入）

进入规则页后：

1. 将「范围」切换为 **全部** 或 **用户**，确认列表中能看到 `java.md`、`python.md`
2. 确认两个规则的「类型」均为 **指定文件生效**（来自规则文件 frontmatter 的 `trigger: glob` 声明）
3. 若列表未更新，点击页面右上角 **刷新** 按钮重新加载

### 使用说明

- 本插件为 rules-only 插件，不含可通过斜杠命令调用的技能
- `rules/java.md` 声明了 `trigger: glob` + `glob: ["**/*.java"]`，属于**指定文件生效**类型：处理 `.java` 文件时自动加载并注入规范
- `rules/python.md` 声明了 `trigger: glob` + `glob: ["**/*.py"]`，属于**指定文件生效**类型：处理 `.py` 文件时自动加载并注入规范
- 如需让规则在**所有对话中始终生效**（不分文件类型），将 frontmatter 改为：

  ```yaml
  ---
  trigger: always_on
  ---
  ```

- 如需临时手动使用（不自动注入），将 frontmatter 改为 `trigger: manual`，在对话中输入 `@rule` 手动引用
- 修改规则文件后无需重启 IDE，下一轮对话即生效；规则管理页点击「刷新」可查看最新规则列表

## 设置说明

无需外部凭据、MCP 服务或环境变量。

## 仓库地址

- https://github.com/zma1234/code-arch-standard.git

## 验证记录

- 已通过 Qoder 官方离线校验器（`validate_qoder_plugin.py`）校验：`ok: true`
- 唯一提示为 "plugin.json does not declare skills"，属 rules-only 插件的正常状态
