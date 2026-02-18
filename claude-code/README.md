# AI-DLC Claude Code セットアップガイド

このディレクトリには、Claude Code用のAI-DLCフレームワーク設定が含まれています。

## インストール方法

プロジェクトのルートディレクトリで以下を実行してください：

```bash
# 1. .claude/commands/ ディレクトリにコマンドをコピー
mkdir -p .claude/commands
cp claude-code/commands/*.md .claude/commands/

# 2. .claude/rules/ ディレクトリにルールをコピー
mkdir -p .claude/rules
cp claude-code/rules/*.md .claude/rules/

# 3. CLAUDE.md をプロジェクトルートにコピー
cp claude-code/CLAUDE.md ./CLAUDE.md
```

または、AI-DLCリポジトリからコピーする場合：

```bash
# AI-DLCリポジトリのパスを指定
AIDLC_REPO=/path/to/ai-dlc-sdd

# コマンドをコピー
mkdir -p .claude/commands
cp $AIDLC_REPO/claude-code/commands/*.md .claude/commands/

# ルールをコピー
mkdir -p .claude/rules
cp $AIDLC_REPO/claude-code/rules/*.md .claude/rules/

# CLAUDE.md をコピー
cp $AIDLC_REPO/claude-code/CLAUDE.md ./CLAUDE.md
```

## ディレクトリ構造

```
claude-code/
├── commands/                    # Claude Code カスタムスラッシュコマンド
│   ├── README.md               # コマンド一覧
│   ├── aidlc-setup.md          # プロジェクト初期化
│   ├── aidlc-inception.md      # Inception Phase
│   ├── aidlc-brownfield.md     # Brown-Field分析
│   ├── aidlc-domain-model.md   # ドメインモデル作成
│   ├── aidlc-architecture.md   # アーキテクチャ設計
│   ├── aidlc-code-generation.md # コード生成
│   ├── aidlc-iac-apis.md       # IaC/REST API生成
│   ├── aidlc-deployment.md     # デプロイメント
│   ├── aidlc-monitoring.md     # 監視設定
│   ├── aidlc-modification.md   # 改修・影響分析
│   ├── aidlc-refactor.md       # リファクタリング
│   ├── aidlc-code-review.md    # コードレビュー
│   ├── aidlc-security-review.md # セキュリティレビュー
│   └── aidlc-build-fix.md      # ビルドエラー修正
├── rules/                       # モジュラールール（→ .claude/rules/ にコピー）
│   ├── README.md               # ルール一覧
│   ├── security.md             # セキュリティガイドライン
│   ├── testing.md              # テスト要件・TDDワークフロー
│   ├── performance.md          # パフォーマンス最適化
│   └── coding-style.md         # コーディングスタイル
├── CLAUDE.md                    # プロジェクト共通原則（→ プロジェクトルートにコピー）
├── AGENTS.md                    # エージェント定義（参照用）
└── README.md                    # このファイル
```

## Cursor版との互換性

このClaude Code版は、`cursor/` ディレクトリのCursor版と完全に互換性があります：

| 項目 | Cursor | Claude Code |
|------|--------|-------------|
| コマンド呼び出し | `@aidlc-setup` | `/aidlc-setup` |
| コマンド配置先 | `.cursor/commands/` | `.claude/commands/` |
| ルール配置先 | `.cursor/rules/*.mdc` | `.claude/rules/*.md` |
| プロジェクト設定 | `.cursorrules` 等 | `CLAUDE.md` |
| 生成ファイル | 同一パス・同一命名規則 | 同一パス・同一命名規則 |
| アーティファクト構造 | `aidlc-docs/`, `BACKEND/` 等 | `aidlc-docs/`, `BACKEND/` 等 |

### ルールファイルの対応

| Claude Code (`.claude/rules/`) | Cursor (`.cursor/rules/`) | フロントマター |
|-------------------------------|--------------------------|---------------|
| `security.md` | `security.mdc` | `paths` ↔ `globs` |
| `testing.md` | `testing.mdc` | `paths` ↔ `globs` |
| `performance.md` | `performance.mdc` | （条件なし＝常時適用） |
| `coding-style.md` | `coding-style.mdc` | `paths` ↔ `globs` |

同じプロジェクトでCursorとClaude Codeの両方を使用する場合、生成されるアーティファクトは共通です。

## 使用方法

Claude Codeのチャットで `/` に続けてコマンド名を入力します：

```
/aidlc-setup
/aidlc-inception "レコメンデーションエンジンを開発する"
/aidlc-domain-model "レコメンデーションアルゴリズム"
```

### Green-Field開発フロー（新規開発）

```
/aidlc-setup
  ↓
/aidlc-inception "<product-description>"
  ↓
/aidlc-domain-model <unit-name>
  ↓
/aidlc-architecture <unit-name>
  ↓
/aidlc-code-generation <unit-name>
  ↓
/aidlc-iac-apis <unit-name> [tool]
  ↓
/aidlc-deployment <unit-name> [environment]
  ↓
/aidlc-monitoring <unit-name>
```

### Brown-Field開発フロー（既存システム拡張）

```
/aidlc-setup
  ↓
/aidlc-brownfield <existing-code-path>
  ↓
/aidlc-inception "<product-description>"
  ↓
（以降、Green-Fieldと同じフロー）
```

### Modification / Refactoring フロー

```
/aidlc-modification "<new-requirement>"
  ↓
（改修計画に従ってConstructionコマンドを実行）

/aidlc-refactor "<target>" [focus-area]
```

## 詳細ドキュメント

- [AGENTS.md](./AGENTS.md) - エージェント定義と専門家の役割
- [commands/README.md](./commands/README.md) - 全コマンドの詳細
- [rules/README.md](./rules/README.md) - ルール一覧と仕様
- [../docs/AI-DLC.md](../docs/AI-DLC.md) - AI-DLC方法論の完全な仕様
