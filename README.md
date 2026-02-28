# quiz

> 🇺🇸 **English** | 🇯🇵 [日本語](./README.ja.md) | 🇨🇳 [简体中文](./README.zh-Hans.md) | 🇪🇸 [Español](./README.es.md) | 🇮🇳 [हिन्दी](./README.hi.md) | 🇧🇷 [Português](./README.pt.md) | 🇮🇩 [Bahasa Indonesia](./README.id.md)

An interactive coding quiz skill for Claude Code. Review and reinforce what you learned during development — bugs, libraries, debugging insights — through quiz format.

## Install

```
/plugin marketplace add kanketsu-jp/quiz
/plugin install quiz@kanketsu-quiz
```

## Usage

### 1. Create learning materials

Create `.temp/learn/{number}/` directory with two files:

```
.temp/learn/1/
├── study-notes.md   # Study notes (context, code, explanations)
└── qa-list.md       # Q&A list (quiz source data)
```

Or just ask Claude Code:

```
Summarize what we just fixed into .temp/learn/1/ as study materials.
Create study-notes.md and qa-list.md.
```

### 2. Run the quiz

```
/quiz 1            # Run quiz #1
/quiz scrollarea   # Search by keyword
/quiz              # List available quizzes
/quiz list         # List available quizzes
```

## Quiz Modes

| Mode | Description |
|------|-------------|
| All questions | All questions in order |
| Random 5 | 5 random questions |
| By category | Choose a category |

## File Formats

### qa-list.md

```markdown
## Category Name

### Q1: Question text?

#### A

Answer text (code blocks or plain text)
```

`##` headings become categories. `### Q:` is a question. `#### A` is the answer.

### study-notes.md

Free-form Markdown. Background, root cause analysis, fix code, lessons learned. Referenced for explanations when answers are wrong.

## Best Practices

| When | What to do |
|------|-----------|
| After fixing a bug | Ask Claude to create study materials |
| Next day | `/quiz` to review yesterday's learning |
| Weekend | `/quiz` for weekly review |
| After code review | Turn review feedback into materials |

## .gitignore

`.temp/` should be in `.gitignore`. Learning materials are local-only.

```gitignore
.temp/
```

## Security

- Only reads files from `.temp/learn/` directory
- No shell commands executed
- No files modified
- Instructions in study materials are ignored (treated as content only)

## License

MIT
