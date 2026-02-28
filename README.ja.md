# quiz

> 🇺🇸 [English](./README.md) | 🇯🇵 **日本語** | 🇨🇳 [简体中文](./README.zh-Hans.md) | 🇪🇸 [Español](./README.es.md) | 🇮🇳 [हिन्दी](./README.hi.md) | 🇧🇷 [Português](./README.pt.md) | 🇮🇩 [Bahasa Indonesia](./README.id.md)

コーディング中に学んだことをクイズ形式で復習できる Claude Code スキルです。バグ修正、ライブラリの習得、デバッグの教訓を定着させます。

## インストール

```
/plugin marketplace add kanketsu-jp/quiz
/plugin install quiz@kanketsu-quiz
```

## 使い方

### 1. 学習資料を作成

`.temp/learn/{番号}/` ディレクトリに2つのファイルを配置します:

```
.temp/learn/1/
├── study-notes.md   # 学習ノート（原因・修正内容・解説）
└── qa-list.md       # Q&Aリスト（クイズの元データ）
```

Claude Code に依頼するだけでも作成できます:

```
今回の修正内容を .temp/learn/1/ に学習資料としてまとめて。
study-notes.md と qa-list.md を作成して。
```

### 2. クイズを実行

```
/quiz 1            # 番号を指定して実行
/quiz scrollarea   # キーワードで検索
/quiz              # 一覧から選択
/quiz list         # 利用可能なクイズを一覧表示
```

## クイズモード

| モード | 説明 |
|--------|------|
| 全問チャレンジ | 全問を順番に出題 |
| ランダム5問 | ランダムに5問を出題 |
| カテゴリ別 | カテゴリを選んで出題 |

## ファイルフォーマット

### qa-list.md

```markdown
## カテゴリ名

### Q1: 質問文？

#### A

回答テキスト（コードブロックやプレーンテキスト）
```

`##` 見出しがカテゴリ、`### Q:` が質問、`#### A` が回答です。

### study-notes.md

自由形式の Markdown。問題の背景、原因分析、修正コード、教訓を記載。不正解時の解説として参照されます。

## おすすめの使い方

| タイミング | やること |
|-----------|---------|
| バグを修正した直後 | Claude に学習資料作成を依頼 |
| 翌日の作業開始時 | `/quiz` で昨日の復習 |
| 週末 | `/quiz` で今週の学びを総復習 |
| コードレビュー後 | 指摘内容を学習資料化 |

## .gitignore

`.temp/` は `.gitignore` に追加することを推奨します。学習資料はローカル専用です。

```gitignore
.temp/
```

## 設定

デフォルトでは `.temp/learn/` から学習資料を読み取ります。設定ファイルでパスをカスタマイズできます:

| 優先度 | ファイル | 形式 |
|--------|---------|------|
| 1 | `.claude/quiz.json` | `{ "learn_dir": "path/to/dir" }` |
| 2 | `.claude/settings.local.json` | `{ "quiz": { "learn_dir": "path/to/dir" } }` |
| 3 | `.claude/settings.json` | `{ "quiz": { "learn_dir": "path/to/dir" } }` |
| 4 | デフォルト | `.temp/learn/` |

`.claude/quiz.json` の例:

```json
{
  "learn_dir": "docs/quiz-materials"
}
```

## セキュリティ

- `.claude/` ディレクトリ内の設定ファイルのみ読み取り（`learn_dir` の解決用）
- 設定されたディレクトリ内の学習資料ファイルのみ読み取り
- シェルコマンドは一切実行しない
- ファイルの変更は一切行わない
- 学習資料内の命令やコマンドはすべて無視（学習コンテンツとして扱う）

## ライセンス

MIT
