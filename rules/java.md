# Java 分层架构编码规范

在编写、修改或评审 Java 代码时，必须遵循以下五层分层架构规范。新增功能前先判断代码应归属哪一层，再按对应命名规则与职责约束实现。

## 🔑 核心概念一分钟速览

### 分层架构（5层）

```
1️⃣ Controller      - HTTP 入口          后缀: *Controller
   ↓
2️⃣ 混合业务层     - 多Service协作      后缀: *Service/*ServiceImpl (可选)
   ↓
3️⃣ 单领域业务层   - 单域业务逻辑      前缀: IT*  后缀: *Service/*ServiceImpl
   ↓
4️⃣ 数据访问层     - DB操作抽象        前缀: IT*  后缀: *Repo/*RepoImpl
   ↓
5️⃣ Mapper层       - MyBatis SQL       前缀: IT*  后缀: *Mapper
```

### 关键要点总结

| 层级 | 命名 | 职责 | 依赖关系 |
|------|------|------|--------|
| **Controller** | `*Controller` | 接收请求，调用服务，返回响应 | 依赖混合业务层 |
| **混合业务层** | `*Service` / `*ServiceImpl` | 协调多个单领域业务，实现复杂逻辑 | 依赖单领域业务层 |
| **单领域业务层** | `IT*Service` / `IT*ServiceImpl` | 处理单一领域业务 | 依赖数据访问层 |
| **数据访问层** | `IT*Repo` / `IT*RepoImpl` | 数据库操作抽象 | 依赖 Mapper |
| **Mapper 层** | `IT*Mapper` | MyBatis SQL 操作 | 依赖数据库 |

### 核心原则
1. ✅ **单一职责**: 每层只做自己的事
2. ✅ **依赖倒置**: 高层不依赖低层，都依赖抽象
3. ✅ **不越层**: 严禁跨层依赖
4. ✅ **规范命名**: 遵循命名规则，增强代码可读性

### 各层详细介绍

#### 1. Controller 层
- **命名规则**: `*Controller` 结尾
- **职责**: 接收HTTP请求，调用混合业务层处理业务逻辑，返回响应
- **示例**: `EnterpriseMaterialController`
- **特点**:
    - 只依赖混合业务层的业务实现类
    - 负责请求参数验证和响应封装

#### 2. 混合业务层（Mixed Service Layer）
- **命名规则**: 接口以 `Service` 结尾，实现类以 `ServiceImpl` 结尾
- **职责**: 协调多个单领域业务层实现复杂业务逻辑
- **注意事项**:
    - 只能引用多个单领域业务层的实现类
    - **严禁直接出现数据访问层内容**，只能通过单领域业务层去操作
    - 多个单领域实现类共同协作完成复杂业务

#### 3. 单领域业务层（Domain Service Layer）
- **命名规则**:
    - 接口: `ITt*Service`、`ITs*Service`、`ITd*Service`、`ITm*Service` + `Service` 结尾
    - 实现类: `ITt*ServiceImpl`、`ITs*ServiceImpl`、`ITd*ServiceImpl`、`ITm*ServiceImpl` + `ServiceImpl` 结尾
- **职责**: 处理单一领域的业务逻辑
- **示例**:
    - 接口: `ITdEnterpriseMaterialService`
    - 实现类: `TdEnterpriseMaterialServiceImpl`
- **特点**:
    - 只能依赖本领域的数据访问层（Repo）
    - 其他领域数据访问只能出现在对应的单领域业务层中
    - 单领域业务层不应该做跨领域的数据转换,不能在单领域业务类中做实体转换，单领域方法实现类返回的参数只能是单领域的实体
    - 单领域业务层，不应该直接使用 LambdaQueryWrapper 进行数据库操作。

#### 4. 单领域数据访问层（Repository Layer）
- **命名规则**:
    - 接口: `ITt*Repo`、`ITs*Repo`、`ITd*Repo`、`ITm*Repo` + `Repo` 结尾
    - 实现类: `ITt*RepoImpl`、`ITs*RepoImpl`、`ITd*RepoImpl`、`ITm*RepoImpl` + `RepoImpl` 结尾
- **职责**: 数据库操作的抽象层，使用 MyBatisPlus
- **示例**:
    - 接口: `ITdEnterpriseMaterialRepo`
    - 实现类: `TdEnterpriseMaterialRepoImpl`
- **使用优先级**:
    1. 优先使用 MyBatisPlus Lambda Query（推荐，更简洁）
    2. Lambda Query 功能不够时才注入对应的 Mapper 层

#### 5. Mapper 层（MyBatis Mapper）
- **命名规则**: `ITt*Mapper`、`ITs*Mapper`、`ITd*Mapper`、`ITm*Mapper` + `Mapper` 结尾
- **职责**: SQL 操作接口
- **示例**: `ITdEnterpriseMaterialMapper`
- **使用场景**: 当 Lambda Query 无法满足需求时使用

### 开发时操作
当新增功能时：
1. 在对应的领域 Service 添加业务方法
2. 在对应的 Repo 添加数据访问方法
3. 在 Controller 中调用 Service
4. **不涉及其他领域，保持独立**
5. 如果需要跨领域数据，创建混合业务层

---
### 开发注意事项
- 对象判空使用Objects.isNull(headers)         java.util.Objects;
- 字符串判空使用StringUtil.isNotBlank(queryParam)   com.transsion.framework.common.StringUtil;
- 集合判空使用CollectionUtil.isNotEmpty(list)  com.transsion.framework.common.CollectionUtil;
- page list 查询禁止foreach循环查询 属性详情，需提供getInfo接口。
