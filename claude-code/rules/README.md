# AI-DLC Rules（ルール）

このディレクトリには、AI-DLCフレームワークで常に従うべきガイドラインが含まれています。

## ルール一覧

### security.md
セキュリティガイドライン。ハードコードされた秘密情報の禁止、入力検証、SQLインジェクション対策など。

### testing.md
テスト要件。80%の最小カバレッジ、TDDワークフロー、テストタイプの定義。

### performance.md
パフォーマンス最適化。コンテキスト管理、並列タスク実行。

### coding-style.md
コーディングスタイル。イミュータビリティ、ファイル構成、エラーハンドリング、入力検証。

## ファイル形式

Claude Codeの `.claude/rules/` 仕様に準拠して、すべてのルールファイルは `.md` 形式（Markdown with YAML frontmatter）を使用しています。

各ファイルにはオプションでYAML frontmatterが含まれています：
- `paths`: 適用するファイルパターン（指定しない場合はすべてのファイルに適用）

## Cursor版との対応

| Claude Code (`.claude/rules/`) | Cursor (`.cursor/rules/`) |
|-------------------------------|--------------------------|
| `security.md` | `security.mdc` |
| `testing.md` | `testing.mdc` |
| `performance.md` | `performance.mdc` |
| `coding-style.md` | `coding-style.mdc` |

主な違い：
- Claude Code: `.md` 拡張子、`paths` フロントマター
- Cursor: `.mdc` 拡張子、`globs` / `alwaysApply` / `type` フロントマター

## 使用方法

これらのルールは、`.claude/rules/` にコピーすると自動的にClaude Codeに読み込まれます。
`paths` フロントマターがあるルールは、該当ファイルを操作する際に適用されます。
`paths` がないルールは、すべてのファイルに対して常に適用されます。

## AI-DLC統合

各ルールは、AI-DLCの特定のフェーズと統合されています：

- **Construction Phase**: コード生成時にすべてのルールが適用される
- **Code Generationコマンド**: 生成されたコードがすべてのルールに準拠していることを確認
- **Commands**: すべてのCommandsがこれらのルールを参照し、専門家の役割を果たす際に従う

## カスタマイズ

プロジェクト固有の要件に合わせて、これらのルールをカスタマイズできます。
