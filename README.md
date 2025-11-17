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

- [Cursor](https://cursor.sh/) エディタがインストールされていること
- プロジェクトのルートディレクトリにアクセスできること

### 導入ステップ

#### 1. フレームワークファイルのコピー

このリポジトリから、以下のファイルとディレクトリを自分のプロジェクトにコピーします：

```bash
# プロジェクトルートに移動
cd /path/to/your/project

# .cursorディレクトリが存在しない場合は作成
mkdir -p .cursor

# エージェント定義ファイルをコピー
cp /path/to/ai-dlc-sdd/cursor/AGENTS.md .cursor/

# コマンドディレクトリを作成
mkdir -p .cursor/commands/aidlc

# コマンドファイルをコピー
cp /path/to/ai-dlc-sdd/cursor/commands/*.md .cursor/commands/aidlc/
```

または、Windows PowerShellの場合：

```powershell
# プロジェクトルートに移動
cd C:\path\to\your\project

# .cursorディレクトリが存在しない場合は作成
New-Item -ItemType Directory -Force -Path .cursor

# エージェント定義ファイルをコピー
Copy-Item "C:\path\to\ai-dlc-sdd\cursor\AGENTS.md" -Destination ".cursor\"

# コマンドディレクトリを作成
New-Item -ItemType Directory -Force -Path .cursor\commands\aidlc

# コマンドファイルをコピー
Copy-Item "C:\path\to\cursor\commands\*.md" -Destination ".cursor\commands\aidlc\"
```

#### 2. コマンドファイルの確認

コピー後、以下のファイルが存在することを確認してください：

```
.cursor/
├── AGENTS.md
└── commands/
    └── aidlc/
        ├── aidlc-setup.md
        ├── aidlc-inception.md
        ├── aidlc-units.md
        ├── aidlc-brownfield.md
        ├── aidlc-domain-model.md
        ├── aidlc-architecture.md
        ├── aidlc-code-generation.md
        ├── aidlc-iac-apis.md
        ├── aidlc-deployment.md
        ├── aidlc-monitoring.md
        └── README.md
```

#### 3. Cursorでの使用

コマンドファイルをコピーした後、Cursorエディタで以下のようにコマンドを使用できます：

```
/aidlc-setup
/aidlc-inception "プロダクトの説明"
```

Cursorは `.cursor/commands/` ディレクトリ内の `.md` ファイルを自動的に認識し、`/` 記号に続けてファイル名（拡張子なし）を入力することでコマンドとして使用できます。

#### 4. プロジェクト構造の初期化（オプション）

フレームワークを使用する前に、プロジェクト構造を初期化することを推奨します：

```
/aidlc-setup
```

このコマンドは、必要なディレクトリ構造を自動的に作成します。

### カスタマイズ

コマンドファイル（`.cursor/commands/aidlc/*.md`）を編集することで、プロジェクトの要件に合わせてフレームワークをカスタマイズできます。

### トラブルシューティング

#### コマンドが認識されない場合

1. `.cursor/commands/aidlc/` ディレクトリが正しく作成されているか確認
2. コマンドファイルが `.md` 拡張子で保存されているか確認
3. Cursorエディタを再起動

#### パスの問題

Windowsでパスに日本語が含まれる場合、PowerShellのエンコーディング設定を確認してください：

```powershell
[Console]::OutputEncoding = [System.Text.Encoding]::UTF8
```

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

### 3. Units作成（オプション）

User StoriesをUnitsにグループ化します：

```
/aidlc-units
```

### 4. Construction Phase（構築フェーズ）

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

### 5. Operations Phase（運用フェーズ）

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
3. /aidlc-units (オプション)
   ↓
4. /aidlc-domain-model <unit-name>
   ↓
5. /aidlc-architecture <unit-name>
   ↓
6. /aidlc-code-generation <unit-name>
   ↓
7. /aidlc-iac-apis <unit-name> <tool>
   ↓
8. /aidlc-deployment <unit-name> <environment>
   ↓
9. /aidlc-monitoring <unit-name>
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
| `/aidlc-units` | User StoriesをUnitsにグループ化 | Inception |
| `/aidlc-brownfield` | 既存コードの分析とモデル化 | Construction (Brown-Field) |
| `/aidlc-domain-model` | Domain Designの作成 | Construction |
| `/aidlc-architecture` | Logical Designの作成 | Construction |
| `/aidlc-code-generation` | コードとユニットテストの生成 | Construction |
| `/aidlc-iac-apis` | IaCとREST APIの生成 | Construction |
| `/aidlc-deployment` | デプロイメントの実行 | Operations |
| `/aidlc-monitoring` | 監視とインシデント管理の設定 | Operations |

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

## エージェント

詳細なエージェント定義については、[.cursor/AGENTS.md](.cursor/AGENTS.md)を参照してください。

## 参考資料

- [AI-DLC Method Definition](docs/AI-DLC.md) - AI-DLC手法の完全な定義

## ライセンス

このプロジェクトは、AI-DLC手法に基づいて実装されています。


