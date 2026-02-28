# Release Notes

## v1.1.0

### 新機能 / New Features

- **学習資料パスのカスタマイズ** — `.claude/quiz.json` 等の設定ファイルで `learn_dir` を指定可能に
- **設定の優先順位** — `.claude/quiz.json` → `.claude/settings.local.json` → `.claude/settings.json` → デフォルト `.temp/learn/`
- **Customizable learning directory** — Configure `learn_dir` in `.claude/quiz.json` or other config files
- **Config priority chain** — `.claude/quiz.json` → `.claude/settings.local.json` → `.claude/settings.json` → default `.temp/learn/`

### セキュリティ / Security

- 設定ファイルは `.claude/` ディレクトリ内のみ読み取り
- `learn_dir` は相対パスのみ許可（`..` や絶対パスは拒否）

---

## v1.0.0

初回リリース。

### 新機能 / New Features

- **インタラクティブクイズスキル** — `/quiz` コマンドでコーディング学習をクイズ形式で復習
- **学習資料からクイズ自動生成** — `.temp/learn/{番号}/qa-list.md` をパースして選択式クイズを出題
- **3つのクイズモード** — 全問チャレンジ / ランダム5問 / カテゴリ別
- **もっともらしい不正解選択肢** — よくある誤解に基づいた選択肢を自動生成
- **即時フィードバック** — 正解・不正解の判定 + study-notes.md からの解説
- **結果サマリー** — 正答率と間違えた問題の一覧を表示
- **再チャレンジ機能** — 間違えた問題だけ再挑戦可能
- **キーワード検索** — `/quiz scrollarea` のようにトピックで検索
- **Claude Code プラグイン** — marketplace からインストール可能
- **読み取り専用** — ファイル変更なし、安全に使用可能
