---
name: springboot-convention-expert
description: 专门用于学习、分析和执行现有 Spring Boot 项目的编码规范。当用户要求“分析代码风格”、“学习项目规范”、“总结编码习惯”，或者在开始编写新代码前需要对齐项目现有 DNA 时，必须触发此技能。Supports tasks like "学习这个项目的编码规范", "分析项目风格", "总结异常处理机制".
---

# Spring Boot Convention Expert

该技能专门用于从现有 Spring Boot 项目中提取、记录并强制执行本地编码标准和架构模式。它确保任何新代码或重构都与项目已建立的“DNA”完美对齐。

## 触发场景 (Trigger Contexts)
- 用户要求：“学习这个项目”、“分析代码风格”、“总结命名规范”。
- 在现有代码库中实现新功能之前。
- 进行代码审查或确保代码符合本地标准时。
- **关键点**: 当用户想了解当前实现的“如何做”和“为什么这么做”时，务必激活。

## 排除规则 (Exclusion Rules)
- **绝对禁止** 学习或参考以下目录中的文件（路径相对于项目根目录）：
    - `**/controller/ifm/**`
    - `**/service/ifm/**`
    - `**/target/**`
    - `**/.idea/**`
    - `**/.gitea/**`
- 将这些目录视为黑盒或特定集成，不代表项目的目标编码标准。

## 学习策略：研究与映射流程 (Study & Map Workflow)
激活学习模式时，请严格执行以下步骤：

### 1. 架构发现 (Architectural Discovery)
- **包策略**: 是按层（controller, service, dao）分包还是按功能（user, order, payment）分包？
- **依赖流**: 各层如何通信？（例如：Controller -> Service -> Mapper）。
- **注入风格**: 倾向于构造函数注入还是字段上的 `@Autowired`？

### 2. 实现模式 (Implementation Patterns)
- **命名约定**: 
    - DTOs: 是 `*DTO`, `*Request/*Response` 还是 `*VO`？
    - Mappers: 是 `*Mapper`, `*Dao` 还是 `*Repository`？
- **Web 层**: 
    - 使用 `@RestController` 还是 `@Controller`？
    - 路径命名风格（kebab-case, camelCase）。
    - 统一响应：找到包装类（如 `Result<T>`, `BaseResponse`）。
- **逻辑层**:
    - Service 接口 vs 直接实现类。
    - 事务边界（`@Transactional` 放在哪里？）。
- **持久层**:
    - MyBatis（XML vs 注解）, JPA, 或 QueryDSL？
    - 基础实体（Base Entity）及公共字段（createdAt, updatedAt）。

### 3. 横切关注点 (Cross-Cutting Concerns)
- **异常处理**: 查找 `@ControllerAdvice`。映射自定义异常体系和错误码命名。
- **日志**: SLF4J 日志记录器的命名和放置位置。
- **校验**: JSR-303 (`@Valid`, `@NotBlank`) 的使用模式。

## 输出结构 (Output Structure)
学习完成后，生成 **项目规范总结报告 (Project Convention Summary)**，包括：
1. **最佳实践示例**: 一段最能代表项目标准的 Controller/Service 代码片段。
2. **命名字典**: 后缀及其含义对照表。
3. **错误处理协议**: 如何抛出和返回错误。
4. **工具栈**: Lombok, MapStruct, Swagger 等的使用情况。

## 执行模式 (Execution Mode)
总结报告生成后，后续所有代码生成必须：
- 使用相同的包结构。
- 遵循命名字典。
- 遵循完全一致的错误处理协议。
- **避免** 引入未经显式要求的新库或新模式。
