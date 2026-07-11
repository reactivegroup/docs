# Reactive Project 贡献指南

您只需要遵循标准的 GitHub 开发流程：使用 GitHub Issues 提交和跟踪 Bug，使用 Pull Requests 合并代码或文档。

秉着对开源友好，我们对贡献者没有具体的要求，你可以通过中文或者英文提问和提交代码都可以。

但请尽一切努力遵循现有的约定和样​​式，以保持代码的可读性。

## 如何贡献

### 先决条件

* JDK 8+（建议 JDK 11+）
* IntelliJ IDEA

### 1. Check Branch

* Branch 名称格式为 `feature/xxx`。
* Feature branch 合并到上游后，请从最新的 `master` checkout 新分支，不要继续在旧分支上提交。

### 2. Pull Request

#### 2.1 Commit Style

PR 标题格式为 `<head>: <subject>`，标题应简洁并准确说明意图。

同时 commit 遵循[通用规范](https://github.com/feflow/git-commit-style-guide)，按照以下规则：

  >- `feat:`      新功能（feature）
  >- `fix:`       修复bug
  >- `docs:`      文档（documentation）
  >- `style:`     格式（不影响代码运行的变动）
  >- `refactor:`  重构（即不是新增功能，也不是修改bug的代码变动）
  >- `perf:`      优化相关，比如提升性能、体验
  >- `test:`      增加测试
  >- `chore:`     构建过程或辅助工具的变动
  >- `revert:`    回滚到上一个版本
  >- `merge:`     代码合并
  >- `sync:`      同步主线或分支的Bug

commit body:

```text
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

您可以借助IDEA插件来规范git commit style：[Git Commit Template](https://plugins.jetbrains.com/plugin/9861-git-commit-template)

### 3. Review and Merge

当 PR 处于可合并状态时，其他成员将进行 Code Review，并将其合并到 `master` 分支。

## 文档变更检查

* 确认 Markdown 相对链接和图片路径有效。
* 技术路线图更新时，同步保留可编辑源文件和预览图。
* 确认引用的文章、图片和课程允许当前使用方式。
* 提交前运行 `git diff --check`。

## 编码约定

### JavaDoc

 * Public API 需要 Javadoc，例如 public 类和 public 方法。
 * 有意义的私有方法也需要 Javadoc。
 * 设计决策和设计模式应在文档中说明。
 * `package` 是 public API 的一部分，应包含 `package-info.java`。
 * 单元测试不需要包含 Javadoc，因为它们不引入新 API 且不包含业务逻辑。

### Packages

* Package包名称以单数表示。
* Package包按domain划分（无util或tool包）。
* Package私有类用于隐藏非public API。
* 在一对一依赖的情况下，内部类优先于package私有类。

### Coding Style

一种编码风格建议是[阿里巴巴Java开发手册](https://github.com/alibaba/p3c)
