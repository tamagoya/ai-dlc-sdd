# AI-Driven Development Lifecycle (AI-DLC) フレームワーク

このプロジェクトは、AI-DLC（AI-Driven Development Lifecycle）に基づいた開発プロセスを実行するためのフレームワークです。

## 概要

AI-DLCは、AIが主導する開発ライフサイクル手法です。従来の人間主導のプロセスとは異なり、AIがワークフローを分解し、推奨を生成し、人間は承認と検証を行います。

### 主な特徴

- **AI主導**: AIがワークフローを分解し、計画を生成
- **人間の承認**: 重要な決定ポイントで人間が承認・検証
- **高速な反復**: 時間単位または日単位の高速なサイクル（Bolts）
- **設計手法の統合**: DDD、BDD、TDDなどの設計手法をコアに統合
- **トレーサビリティ**: すべてのアーティファクトがリンクされ、前後のトレーサビリティを確保

## インストール・導入

自分のプロジェクトにAI-DLCフレームワークを導入する手順です。

### 前提条件

以下のいずれかのツールがインストールされていること：
- [Cursor](https://cursor.sh/) エディタ
- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) CLI

### 導入ステップ（Cursor）

#### 1. フレームワークファイルのコピー

```bash
cd /path/to/your/project

mkdir -p .cursor
cp /path/to/ai-dlc-sdd/cursor/AGENTS.md .cursor/

mkdir -p .cursor/commands/aidlc
cp /path/to/ai-dlc-sdd/cursor/commands/*.md .cursor/commands/aidlc/
```

#### 2. 使用方法

Cursorエディタのチャットで `@` に続けてコマンド名を入力：

```
@aidlc-setup
@aidlc-inception "プロダクトの説明"
```

### 導入ステップ（Claude Code）

#### 1. フレームワークファイルのコピー

```bash
cd /path/to/your/project

# コマンドをコピー
mkdir -p .claude/commands
cp /path/to/ai-dlc-sdd/claude-code/commands/*.md .claude/commands/

# ルールをコピー
mkdir -p .claude/rules
cp /path/to/ai-dlc-sdd/claude-code/rules/*.md .claude/rules/

# CLAUDE.md をプロジェクトルートにコピー
cp /path/to/ai-dlc-sdd/claude-code/CLAUDE.md ./CLAUDE.md
```

#### 2. 使用方法

Claude Codeのチャットで `/` に続けてコマンド名を入力：

```
/aidlc-setup
/aidlc-inception "プロダクトの説明"
```

### Cursor / Claude Code 互換性

両ツールで**同じプロジェクト**を扱えます。生成されるアーティファクト（`aidlc-docs/`、`BACKEND/`等）はすべて共通です。

| 項目 | Cursor | Claude Code |
|------|--------|-------------|
| コマンド呼び出し | `@aidlc-*` | `/aidlc-*` |
| コマンド配置先 | `.cursor/commands/` | `.claude/commands/` |
| ルール配置先 | `.cursor/rules/*.mdc` | `.claude/rules/*.md` |
| プロジェクト設定 | `.cursorrules` 等 | `CLAUDE.md` |
| 生成アーティファクト | 同一 | 同一 |

### プロジェクト構造の初期化

フレームワーク導入後、最初に以下を実行してプロジェクト構造を初期化してください：

```
/aidlc-setup
```

### カスタマイズ

- Cursor: `.cursor/commands/aidlc/*.md` を編集
- Claude Code: `.claude/commands/*.md` を編集

## プロジェクト構造

```
aidlc-docs/
├── requirements/          # 要件ドキュメント
├── story-artifacts/       # User Stories
├── design-artifacts/      # 設計ドキュメント
│   ├── domain-models/    # ドメインモデル
│   ├── logical-designs/  # 論理設計
│   ├── static-models/    # 静的モデル（Brown-Field用）
│   ├── dynamic-models/   # 動的モデル（Brown-Field用）
│   ├── adrs/             # Architecture Decision Records
│   └── units/            # Units定義
├── plans/                # 計画ドキュメント
└── prompts.md           # プロンプト履歴

BACKEND/                  # バックエンドコード
FRONTEND/                # フロントエンドコード（該当する場合）
DEPLOYMENT/              # デプロイメント設定
ARCHITECTURE/            # アーキテクチャドキュメント
UNITS/                   # Units定義
```

## クイックスタート

### 1. セットアップ

プロジェクトの初期セットアップを行います：

```
/aidlc-setup
```

このコマンドは、必要なディレクトリ構造とファイルを作成します。

### 2. Inception Phase（開始フェーズ）

プロダクトの説明からUser StoriesとUnitsを作成します：

```
/aidlc-inception "クロスセル商品のレコメンデーションエンジンを開発する"
```

このコマンドは以下を実行します：
- Intentの明確化（質問生成）
- User Storiesの作成
- NFRs（非機能要件）の定義
- Risk（リスク）の記述
- Unitsへの分解
- PRFAQの生成（オプション）
- Measurement Criteria（測定基準）の定義
- Suggested Bolts（推奨ボルト）の生成

### 3. Construction Phase（構築フェーズ）

#### Domain Model作成

指定されたUnitのDomain Designを作成します：

```
/aidlc-domain-model "レコメンデーションアルゴリズム"
```

#### Architecture設計

Domain DesignをLogical Designに変換し、NFRsを満たすためのアーキテクチャパターンを適用します：

```
/aidlc-architecture "レコメンデーションアルゴリズム"
```

#### コード生成

Domain ModelとLogical Designに基づいて、実行可能なコードとユニットテストを生成します：

```
/aidlc-code-generation "レコメンデーションアルゴリズム"
```

#### IaC/REST APIs生成

Infrastructure as CodeとREST APIを生成します：

```
/aidlc-iac-apis "レコメンデーションアルゴリズム" terraform
```

### 4. Operations Phase（運用フェーズ）

#### デプロイメント

Deployment Unitsをパッケージ化し、環境にデプロイします：

```
/aidlc-deployment "レコメンデーションアルゴリズム" staging
```

#### 監視

デプロイされたシステムの監視、メトリクス分析、インシデント管理を設定します：

```
/aidlc-monitoring "レコメンデーションアルゴリズム"
```

## Brown-Field開発

既存システムに対して新機能を追加する場合：

### 1. 既存コードの分析

既存コードを高レベルなモデリング表現に変換します：

```
/aidlc-brownfield "BACKEND/legacy-system"
```

このコマンドは以下を実行します：
- 既存コードの分析
- 静的モデル（コンポーネント、責任、関係）の作成
- 動的モデル（ユースケース実現のための相互作用）の作成
- コンテキストの構築

### 2. 通常のConstruction Phase

Brown-Field分析後、通常のConstruction Phaseを実行します。

## 開発フロー

### Green-Field開発フロー

```
1. /aidlc-setup
   ↓
2. /aidlc-inception "<product-description>"
   ↓
3. /aidlc-domain-model <unit-name>
   ↓
4. /aidlc-architecture <unit-name>
   ↓
5. /aidlc-code-generation <unit-name>
   ↓
6. /aidlc-iac-apis <unit-name> <tool>
   ↓
7. /aidlc-deployment <unit-name> <environment>
   ↓
8. /aidlc-monitoring <unit-name>
```

### Brown-Field開発フロー

```
1. /aidlc-setup
   ↓
2. /aidlc-brownfield <existing-code-path>
   ↓
3. /aidlc-inception "<product-description>"
   ↓
4. (Construction PhaseはGreen-Fieldと同じ)
```

## コマンド一覧

| コマンド | 説明 | フェーズ |
|---------|------|---------|
| `/aidlc-setup` | プロジェクトの初期セットアップ | Setup |
| `/aidlc-inception` | IntentをUser StoriesとUnitsに分解 | Inception |
| `/aidlc-brownfield` | 既存コードの分析とモデル化 | Construction (Brown-Field) |
| `/aidlc-domain-model` | Domain Designの作成 | Construction |
| `/aidlc-architecture` | Logical Designの作成 | Construction |
| `/aidlc-code-generation` | コードとユニットテストの生成 | Construction |
| `/aidlc-iac-apis` | IaCとREST APIの生成 | Construction |
| `/aidlc-deployment` | デプロイメントの実行 | Operations |
| `/aidlc-monitoring` | 監視とインシデント管理の設定 | Operations |
| `/aidlc-modification` | 追加改修の影響分析と計画 | Modification |
| `/aidlc-refactor` | コードと設計のリファクタリング | Improvement |

## アーティファクト

### Inception Phase

- **Intent**: 高レベルの目的の記述
- **User Stories**: 機能要件の記述
- **NFRs**: 非機能要件の定義
- **Risks**: リスクの記述
- **Units**: 独立して構築可能な作業単位
- **PRFAQ**: ビジネス意図の要約（オプション）
- **Measurement Criteria**: 測定基準の定義
- **Suggested Bolts**: 推奨される短期間の反復サイクル

### Construction Phase

- **Domain Design**: ビジネスロジックのモデル（インフラストラクチャから独立）
- **Logical Design**: NFRsを満たすためのアーキテクチャパターンを適用した設計
- **Code and Unit Tests**: 実行可能なコードとユニットテスト
- **ADRs**: Architecture Decision Records

### Operations Phase

- **Deployment Units**: パッケージ化された実行可能コード、設定、インフラストラクチャ
- **Monitoring Dashboards**: 監視ダッシュボード
- **Incident Runbooks**: インシデント対応プレイブック

## 原則

### 計画ファーストアプローチ

すべてのエージェントは、作業を開始する前に計画を作成し、人間の承認を待ちます。

### チェックボックス付き計画

すべての計画は、チェックボックス付きのMarkdownファイルとして作成され、各ステップの完了時にチェックされます。

### 人間の承認が必要なポイント

- 計画の承認
- 重要な設計決定
- リスクの評価
- デプロイメントの承認

### コンテキストメモリ

すべてのアーティファクトは永続化され、後続のステップで参照される「コンテキストメモリ」として機能します。

### トレーサビリティ

すべてのアーティファクトはリンクされ、前後のトレーサビリティが確保されます（例：ドメインモデル要素とUser Storiesの関連付け）。

## 専門家の役割

詳細な専門家の役割定義については、以下を参照してください：
- Cursor版: [cursor/AGENTS.md](cursor/AGENTS.md)
- Claude Code版: [claude-code/AGENTS.md](claude-code/AGENTS.md)

専門家の役割は、各コマンド内で実装されています。

## 参考資料

- [AI-DLC Method Definition](docs/AI-DLC.md) - AI-DLC手法の完全な定義
- [Everything Claude Code統合提案](docs/INTEGRATION_PROPOSAL.md) - Everything Claude Codeのテクニック統合提案

## Everything Claude Code統合

このフレームワークは、[Everything Claude Code](https://github.com/affaan-m/everything-claude-code)の実践的なテクニックを統合しています：

- **Rules（ルール）**: セキュリティ、テスト、パフォーマンス、コーディングスタイルのガイドライン
- **専門家の役割**: コードレビュー、セキュリティレビュー、TDDガイドなどの専門家の役割（Commands内に統合）
- **パフォーマンス最適化**: モデル選択戦略、コンテキストウィンドウ管理

詳細は[統合提案ドキュメント](docs/INTEGRATION_PROPOSAL.md)を参照してください。

## ライセンス

このプロジェクトは、AI-DLC手法に基づいて実装されています。



