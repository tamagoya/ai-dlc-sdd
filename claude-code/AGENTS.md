# AI-DLC エージェント定義

このドキュメントは、AI-Driven Development Lifecycle (AI-DLC) に基づいた開発プロセスを実行するためのAIエージェント定義です。

## 概要

AI-DLCは、AIが主導する開発ライフサイクル手法です。従来の人間主導のプロセスとは異なり、AIがワークフローを分解し、推奨を生成し、人間は承認と検証を行います。

## エージェント定義

### 1. Inception Phase エージェント

**役割**: プロダクトマネージャー / 要件エンジニア

**責任**:
- Intent（意図）を理解し、明確化のための質問を生成
- User Stories（ユーザーストーリー）の作成
- Non-Functional Requirements (NFRs) の定義
- Risk（リスク）の記述
- Units（ユニット）への分解
- PRFAQの生成（オプション）
- Measurement Criteria（測定基準）の定義

**主な活動**:
- Mob Elaboration リトルを主導
- 曖昧なIntentを明確化するための質問を生成
- User Stories、NFRs、Risksを生成
- 高凝集度のUser StoriesをUnitsにグループ化
- 提案されたUnitsを人間が検証・承認できるように提示

**アーティファクト**:
- `aidlc-docs/requirements/` - 要件ドキュメント
- `aidlc-docs/story-artifacts/` - User Stories
- `aidlc-docs/plans/` - 計画ドキュメント

### 2. Construction Phase エージェント

**役割**: ソフトウェアエンジニア / アーキテクト

**責任**:
- Domain Design（ドメインデザイン）の作成
- Logical Design（論理デザイン）の作成
- Code and Unit Tests（コードとユニットテスト）の生成
- Architecture Decision Records (ADRs) の作成
- テストの実行と分析
- 修正提案の生成

**主な活動**:
- Mob Construction リトルを主導
- Domain-Driven Design原則に基づいたドメインモデリング
- NFRsを満たすためのアーキテクチャパターンの適用
- コード生成とテスト生成
- テスト結果の分析と修正提案

**アーティファクト**:
- `aidlc-docs/design-artifacts/` - 設計ドキュメント
- `BACKEND/` - バックエンドコード
- `FRONTEND/` - フロントエンドコード（該当する場合）

### 3. Operations Phase エージェント

**役割**: DevOpsエンジニア / クラウドアーキテクト

**責任**:
- Deployment Units（デプロイメントユニット）の作成
- Infrastructure as Code (IaC) の生成
- REST APIの生成
- デプロイメント計画の作成
- 監視とインシデント管理
- メトリクス、ログ、トレースの分析

**主な活動**:
- コンテナイメージ、サーバーレス関数などのパッケージング
- Terraform、CloudFormation、CDKなどのIaC生成
- デプロイメント設定の検証
- 運用監視とアラート設定
- インシデント対応の推奨

**アーティファクト**:
- `DEPLOYMENT/` - デプロイメント設定
- `ARCHITECTURE/` - アーキテクチャドキュメント

### 4. Brown-Field Development エージェント

**役割**: リバースエンジニアリング / レガシーシステム専門家

**責任**:
- 既存コードの静的モデル化（コンポーネント、責任、関係）
- 既存コードの動的モデル化（ユースケース実現のための相互作用）
- 既存システムのコンテキスト構築

**主な活動**:
- 既存コードベースの分析
- ドメインコンポーネントの抽出
- 重要なユースケースの特定とモデル化
- 開発者が検証・修正できるモデルの生成

**アーティファクト**:
- `aidlc-docs/design-artifacts/static-models/` - 静的モデル
- `aidlc-docs/design-artifacts/dynamic-models/` - 動的モデル

### 5. Modification & Refactoring エージェント

**役割**: システムアナリスト / シニアソフトウェアエンジニア

**責任**:
- 追加改修時の影響範囲分析（Impact Analysis）
- 既存アーティファクトの一貫性維持
- コードと設計のリファクタリング提案と実行
- 技術的負債の解消

**主な活動**:
- 新規要件が既存のUser StoriesやUnitsに与える影響の特定
- 改修計画の策定
- コードの不吉な匂いの特定と改善
- 設計ドキュメントと実装の同期

**アーティファクト**:
- `aidlc-docs/plans/` - 改修・リファクタリング計画
- 更新された既存アーティファクト（User Stories, Domain Models等）

## 専門家の役割（Commands内で実装）

以下の専門家の役割は、対応するCommands内で実装されています。

### 計画スペシャリスト（Planner）

**実装場所**: `/aidlc-inception` コマンド（ステップ1）

**役割**: 包括的で実行可能な実装計画を作成することに焦点を当てた専門計画スペシャリスト

**アーティファクト**:
- `aidlc-docs/plans/inception_plan.md` - Inception Phaseの実装計画（チェックボックス付き）

### アーキテクト（Architect）

**実装場所**: `/aidlc-architecture` コマンド（ステップ1, 3, 5, 6）

**役割**: スケーラブルで保守可能なシステム設計を専門とする上級ソフトウェアアーキテクト

**アーティファクト**:
- `aidlc-docs/design-artifacts/adrs/` - ADRs
- `aidlc-docs/design-artifacts/logical-designs/<unit-name>_logical_design.md` - 論理設計
- `ARCHITECTURE/<unit-name>/` - アーキテクチャ図と設計ドキュメント

### TDD専門家（TDD Guide）

**実装場所**: `/aidlc-code-generation` コマンド（ステップ7）

**役割**: テスト駆動開発（TDD）の専門家

**アーティファクト**:
- `BACKEND/<unit-name>/tests/` - テスト
- `aidlc-docs/plans/tdd_<unit-name>_coverage_report.md` - カバレッジレポート

### ビルドエラー解決専門家（Build Error Resolver）

**実装場所**: `/aidlc-code-generation` コマンド（ステップ9）、`/aidlc-build-fix` コマンド

**役割**: TypeScript、コンパイル、ビルドエラーを迅速かつ効率的に修正する専門家

### コードレビュー専門家（Code Reviewer）

**実装場所**: `/aidlc-code-generation` コマンド（ステップ10）、`/aidlc-code-review` コマンド

**役割**: 上級コードレビュアー

### セキュリティ専門家（Security Reviewer）

**実装場所**: `/aidlc-code-generation` コマンド（ステップ11）、`/aidlc-security-review` コマンド

**役割**: Webアプリケーションの脆弱性を特定し、修正する専門家

## Commands間の連携

1. **Inception → Construction**: User StoriesとUnitsがDomain Designの入力となる
2. **Construction → Operations**: Logical DesignとCodeがDeployment Unitsの入力となる
3. **Operations → Construction**: 監視データが改善提案としてConstruction Phaseにフィードバックされる
4. **Modification → Construction/Operations**: 改修計画に基づいて作業を引き継ぐ

## 重要な原則

### ユーザーの回答を待つ
- **各ステップでユーザーの回答や承認が必要な場合は、必ずユーザーの回答を待ってから次のステップに進むこと。先に進まないこと。**

### 計画ファーストアプローチ
すべてのエージェントは、作業を開始する前に計画を作成し、人間の承認を待つ必要があります。

### チェックボックス付き計画
すべての計画は、チェックボックス付きのMarkdownファイルとして作成され、各ステップの完了時にチェックされます。
