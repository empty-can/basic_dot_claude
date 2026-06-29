# basic_dot_claude — 共有 `.claude` 本体

Claude Code を使う作業の種別を問わず使える、**汎用的な共有 `.claude` フォルダの本体リポジトリ**。
このリポジトリの中身がそのまま利用側プロジェクトの `.claude/` になる（git submodule として取り込む、
または中身をコピーする）。

## 位置づけ（配布フロー）

- **供給元（開発）**: `base-dev-kit-for-cc` で開発した `.claude` 資産を `publish-share` で本リポへ反映。
- **本体（このリポ）**: 配る `.claude` の単一の真実源。`main` が公開基準。
- **利用側**: ひな型ハブ `basic_cc_project` が本リポを `.claude` submodule として取り込み、
  作業リポは `--add-dir <ハブ>` で参照、または `.claude` の中身をコピーして利用する。

## 構成

| 要素 | 用途 |
|---|---|
| `CLAUDE.md` | チーム共通指示（利用側で `.claude/CLAUDE.md` として自動ロード） |
| `settings.json` | permissions / hooks / env / 層2 起動装置（`enabledPlugins` 等）の project 設定 |
| `skills/` | スキル（`<name>/SKILL.md`） |
| `agents/` | サブエージェント定義（`<name>.md`） |
| `commands/` | スラッシュコマンド（新規は `skills/` 推奨） |
| `rules/` | path-scoped 規約（`paths:` frontmatter で条件ロード） |
| `hooks/` | フック用スクリプト（`settings.json` から `$CLAUDE_PROJECT_DIR/.claude/hooks/...` で参照） |
| `output-styles/` | 出力スタイル |

> 現在は**初期スキャフォールド**（各フォルダは空・`.gitkeep` のみ、`CLAUDE.md`/`settings.json` は空）。
> 実資産は供給元から `publish-share` で充填する。
