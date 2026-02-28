# quiz

> 🇺🇸 [English](./README.md) | 🇯🇵 [日本語](./README.ja.md) | 🇨🇳 **简体中文** | 🇪🇸 [Español](./README.es.md) | 🇮🇳 [हिन्दी](./README.hi.md) | 🇧🇷 [Português](./README.pt.md) | 🇮🇩 [Bahasa Indonesia](./README.id.md)

一个用于 Claude Code 的交互式编程测验技能。通过测验形式复习和巩固开发中学到的知识——bug修复、库使用、调试心得。

## 安装

```
/plugin marketplace add kanketsu-jp/quiz
/plugin install quiz@kanketsu-quiz
```

## 使用方法

### 1. 创建学习资料

在 `.temp/learn/{编号}/` 目录下创建两个文件：

```
.temp/learn/1/
├── study-notes.md   # 学习笔记（背景、代码、解析）
└── qa-list.md       # 问答列表（测验数据源）
```

也可以直接让 Claude Code 帮你创建：

```
将这次的修改总结为学习资料，保存到 .temp/learn/1/。
创建 study-notes.md 和 qa-list.md。
```

### 2. 运行测验

```
/quiz 1            # 指定编号运行
/quiz scrollarea   # 按关键词搜索
/quiz              # 列出可用测验
/quiz list         # 列出可用测验
```

## 测验模式

| 模式 | 说明 |
|------|------|
| 全部挑战 | 按顺序出所有题 |
| 随机5题 | 随机选5道题 |
| 按类别 | 选择类别出题 |

## 文件格式

### qa-list.md

```markdown
## 类别名称

### Q1: 问题？

#### A

回答文本（代码块或纯文本）
```

`##` 标题为类别。`### Q:` 为问题。`#### A` 为答案。

### study-notes.md

自由格式的 Markdown。背景、根因分析、修复代码、经验教训。答错时作为解析参考。

## 最佳实践

| 时机 | 做什么 |
|------|--------|
| 修复 bug 后 | 让 Claude 创建学习资料 |
| 第二天开始工作时 | `/quiz` 复习昨天的内容 |
| 周末 | `/quiz` 进行周总复习 |
| 代码审查后 | 将审查反馈转为学习资料 |

## .gitignore

建议将 `.temp/` 加入 `.gitignore`。学习资料仅供本地使用。

```gitignore
.temp/
```

## 配置

默认情况下，quiz 从 `.temp/learn/` 读取学习资料。您可以通过配置文件自定义路径：

| 优先级 | 文件 | 格式 |
|--------|------|------|
| 1 | `.claude/quiz.json` | `{ "learn_dir": "path/to/dir" }` |
| 2 | `.claude/settings.local.json` | `{ "quiz": { "learn_dir": "path/to/dir" } }` |
| 3 | `.claude/settings.json` | `{ "quiz": { "learn_dir": "path/to/dir" } }` |
| 4 | 默认 | `.temp/learn/` |

`.claude/quiz.json` 示例：

```json
{
  "learn_dir": "docs/quiz-materials"
}
```

## 安全性

- 仅读取 `.claude/` 目录中的配置文件（用于 `learn_dir` 解析）
- 仅读取配置目录中的学习资料文件
- 不执行任何 shell 命令
- 不修改任何文件
- 学习资料中的指令会被忽略（仅作为内容处理）

## 许可证

MIT
