# AI-DLC (AI-Driven Development Lifecycle) プロジェクトガイドライン

このプロジェクトはAI-DLC（AI-Driven Development Lifecycle）フレームワークに従って開発を行います。
AIが主導する開発ライフサイクル手法であり、AIがワークフローを分解し、推奨を生成し、人間は承認と検証を行います。

詳細なルール（セキュリティ、テスト、パフォーマンス、コーディングスタイル）は `.claude/rules/` を参照してください。

## コマンド一覧

AI-DLCのコマンドは `/aidlc-*` で利用できます。詳細は `.claude/commands/` を参照してください。

| コマンド | フェーズ | 説明 |
|---------|--------|------|
| `/aidlc-setup` | セットアップ | プロジェクト構造の初期化 |
| `/aidlc-inception` | Inception | IntentをUser StoriesとUnitsに分解 |
| `/aidlc-brownfield` | Construction | 既存コードの分析とモデル化 |
| `/aidlc-domain-model` | Construction | DDD基盤のDomain Design作成 |
| `/aidlc-architecture` | Construction | Logical Design・ADR作成 |
| `/aidlc-code-generation` | Construction | TDDベースのコード生成 |
| `/aidlc-iac-apis` | Construction | IaCとREST API生成 |
| `/aidlc-deployment` | Operations | パッケージ化とデプロイ |
| `/aidlc-monitoring` | Operations | 監視・メトリクス設定 |
| `/aidlc-modification` | Improvement | 影響分析と改修計画 |
| `/aidlc-refactor` | Improvement | リファクタリング |
| `/aidlc-code-review` | Support | コードレビュー |
| `/aidlc-security-review` | Support | セキュリティレビュー |
| `/aidlc-build-fix` | Support | ビルドエラー修正 |

## 共通原則

### ユーザーの回答を待つ
- **各ステップでユーザーの回答や承認が必要な場合は、必ずユーザーの回答を待ってから次のステップに進むこと。先に進まないこと。**
- 質問を提示した場合は、ユーザーからの回答を待ってから処理を続行する
- 承認を求めた場合は、ユーザーからの承認が得られるまで次のステップに進まない
- 修正提案を提示した場合は、ユーザーからの指示を待ってから修正を実行する

### 計画ファーストアプローチ
すべてのコマンドは、作業を開始する前に計画を作成し、人間の承認を待つ必要があります。

### チェックボックス付き計画
すべての計画は、チェックボックス付きのMarkdownファイルとして作成され、各ステップの完了時にチェックされます。

### 人間の承認が必要なポイント
- 計画の承認
- 重要な設計決定
- リスクの評価
- デプロイメントの承認
- PRFAQの生成（オプション）
- 質問への回答
- 修正提案への対応

### コンテキストメモリ
すべてのアーティファクトは永続化され、後続のステップで参照される「コンテキストメモリ」として機能します。

### トレーサビリティ
すべてのアーティファクトはリンクされ、前後のトレーサビリティが確保されます。
