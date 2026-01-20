# AI-DLC コマンド一覧

このディレクトリには、AI-DLCフレームワークで使用可能なすべてのコマンドが含まれています。

## セットアップ

### `@aidlc-setup`
プロジェクトの初期セットアップを行います。

## Inception Phase（開始フェーズ）

### `@aidlc-inception "<product-description>"`
IntentをUser StoriesとUnitsに分解します。

### `@aidlc-units [user-stories-file]`
User StoriesをUnitsにグループ化します。

## Construction Phase（構築フェーズ）

### `@aidlc-brownfield <existing-code-path>`
既存コードを高レベルなモデリング表現に変換します（Brown-Field開発用）。

### `@aidlc-domain-model <unit-name>`
指定されたUnitのDomain Designを作成します。

### `@aidlc-architecture <unit-name>`
Domain DesignをLogical Designに変換し、NFRsを満たすためのアーキテクチャパターンを適用します。

### `@aidlc-code-generation <unit-name>`
Domain ModelとLogical Designに基づいて、実行可能なコードとユニットテストを生成します。

### `@aidlc-iac-apis <unit-name> [tool]`
Infrastructure as CodeとREST APIを生成します。`tool`は`terraform`、`cdk`、`cloudformation`のいずれかです。

## Operations Phase（運用フェーズ）

### `@aidlc-deployment <unit-name> [environment]`
Deployment Unitsをパッケージ化し、指定された環境（`staging`または`production`）にデプロイします。

### `@aidlc-monitoring <unit-name>`
デプロイされたシステムの監視、メトリクス分析、インシデント管理を設定します。

## Modification & Improvement（改修・改善）

### `@aidlc-modification "<new-requirement>"`
追加改修や要件変更が発生した際に、既存のアーティファクトへの影響を分析し、改修計画を策定します。

### `@aidlc-refactor "<target>"`
既存のコードベースと設計を分析し、リファクタリングを提案・実行します。

## 専門家の役割

Cursor公式ドキュメントのベストプラクティスに従い、エージェントを呼び出すのではなく、Commands内で直接専門家の役割を果たすように設計されています。

多くのコマンドは、特定の専門家の役割を内包しています：

- **`/aidlc-inception`**: 計画スペシャリストとして実装計画を作成
- **`/aidlc-architecture`**: アーキテクトとしてアーキテクチャ設計を実行
- **`/aidlc-code-generation`**: TDD専門家、ビルドエラー解決専門家、コードレビュー専門家、セキュリティ専門家として複数の役割を果たす
- **`/aidlc-code-review`**: コードレビュー専門家としてレビューを実行
- **`/aidlc-security-review`**: セキュリティ専門家としてセキュリティレビューを実行
- **`/aidlc-build-fix`**: ビルドエラー解決専門家としてエラーを修正

詳細は [AGENTS.md](../AGENTS.md) を参照してください。

## 使用方法

各コマンドは、Cursorエディタのチャットで`@`記号に続けてコマンド名を入力することで実行できます。

例：
```
@aidlc-setup
@aidlc-inception "レコメンデーションエンジンを開発する"
@aidlc-domain-model "レコメンデーションアルゴリズム"
```

各コマンドの詳細については、対応する`.md`ファイルを参照してください。

