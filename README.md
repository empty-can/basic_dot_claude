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
| `rules/` | path-scoped 規約（`paths:` frontmatter で条件ロード） |
| `hooks/` | フック用スクリプト（`settings.json` から `$CLAUDE_PROJECT_DIR/.claude/hooks/...` で参照） |
| `output-styles/` | 出力スタイル |
| `templates/` | skill 依頼書などのテンプレート |
| `launcher/` | 起動ランチャーの**部品**（`setup-environment.{sh,ps1}`・各テンプレート）。**本体 `start_claude_code.{sh,ps1}` は `.claude/` の外**にあり本リポには含まれない ―― ひな型ハブ `basic_cc_project` がルート直下に持つ |
| `.gitignore` / `.gitattributes` | 配布先での個人実体の除外・改行固定（payload に同乗する統制ファイル） |

> **配布実体はこのリポの `main` に反映済み**（供給元 `base-dev-kit-for-cc` の `publish-share` が充填する）。
> ⚠ **利用者が編集してもここでは変わらない** ―― 資産の変更は必ず供給元で行い `publish-share` で再配布する。
> 本リポへ手で commit すると、次の publish（ミラー）で payload に無いものは消える。
> **例外は `README.md` / `LICENSE` / `.gitignore` / `.gitattributes`**（publish の keep-list で保護されるが、
> `.gitignore` / `.gitattributes` は payload 側が上書きするため実質は供給元が正）。この `README.md` は
> keep-list で守られるので、供給元からは更新されない ―― 実態とズレたら本リポへ直接コミットして直す。
