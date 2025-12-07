# 代码分析技能

用于分析 TypeScript、Python 和 Java 项目的代码结构、模式和质量的技能。

## 能力

- 项目结构分析
- 依赖映射
- 模式识别
- 复杂度度量
- 代码质量评估

## 支持的语言

| 语言 | 文件扩展名 | 框架 |
|------|------------|------|
| TypeScript | `.ts`, `.tsx` | React, Next.js, NestJS |
| JavaScript | `.js`, `.jsx` | Express, Vue |
| Python | `.py` | Django, FastAPI, Flask |
| Java | `.java` | Spring Boot, Jakarta EE |

## 分析类型

### 1. 结构分析

分析项目组织：
- 目录结构
- 模块组织
- 文件关系

### 2. 依赖分析

映射依赖关系：
- 外部包
- 内部导入
- 循环依赖

### 3. 模式分析

识别模式：
- 架构模式（MVC、六边形等）
- 设计模式（工厂、策略等）
- 反模式

### 4. 复杂度分析

计算度量指标：
- 圈复杂度
- 代码行数
- 函数/方法数量
- 嵌套深度

### 5. API 分析

提取 API 信息：
- 端点和路由
- 请求/响应类型
- 认证要求

## 用法

### TypeScript 分析

```bash
# 查找所有 TypeScript 文件
find src -name "*.ts" -o -name "*.tsx"

# 提取导出
grep -r "export" --include="*.ts" src/

# 查找依赖
cat package.json | jq '.dependencies'
```

### Python 分析

```bash
# 查找所有 Python 文件
find . -name "*.py" -not -path "./.venv/*"

# 提取类
grep -r "class " --include="*.py" .

# 查找导入
grep -r "^import\|^from" --include="*.py" .
```

### Java 分析

```bash
# 查找所有 Java 文件
find src -name "*.java"

# 提取类
grep -r "public class\|public interface" --include="*.java" .

# 查找注解
grep -r "@" --include="*.java" src/
```

## 输出格式

```markdown
# 代码分析报告

## 项目概述
- 类型：[TypeScript/Python/Java]
- 文件数：[数量]
- 代码行数：[数量]

## 结构
[目录树]

## 依赖
[依赖列表]

## 模式
[识别的模式]

## 度量
[复杂度度量]

## 建议
[改进建议]
```

## 集成

- 被审查代理用于获取上下文
- 被文档代理用于分析
- 被规划代理用于范围估算
