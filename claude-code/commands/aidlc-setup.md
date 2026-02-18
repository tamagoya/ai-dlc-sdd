AI-DLCセットアップエージェントとして、以下の手順でプロジェクトの初期セットアップを行ってください。

## 作成するディレクトリ構造

```
aidlc-docs/
├── requirements/          # 要件ドキュメント
├── story-artifacts/       # User Stories
├── design-artifacts/      # 設計ドキュメント
│   ├── static-models/    # 静的モデル（Brown-Field用）
│   └── dynamic-models/   # 動的モデル（Brown-Field用）
├── plans/                # 計画ドキュメント
└── prompts.md           # プロンプト履歴

BACKEND/                  # バックエンドコード
FRONTEND/                # フロントエンドコード（該当する場合）
DEPLOYMENT/              # デプロイメント設定
ARCHITECTURE/            # アーキテクチャドキュメント
UNITS/                   # Units定義
```

## 実行手順

### ステップ1: 計画の作成
1. `aidlc-docs/plans/setup_plan.md` にセットアップ計画を作成
2. チェックボックス付きで各ステップを記載
3. ユーザーの承認を待つ

### ステップ2: ディレクトリ構造の作成
1. 上記のディレクトリ構造をすべて作成
2. 各ディレクトリに `.gitkeep` ファイルを配置（空ディレクトリをGitに含めるため）

### ステップ3: 初期ファイルの作成
1. `aidlc-docs/prompts.md` を初期化
2. 必要に応じてREADMEファイルを作成

### ステップ4: 確認
1. 作成された構造を確認し、ユーザーに報告

## 注意事項
- 既存のディレクトリやファイルを上書きしない
- 各ステップの完了時に計画ファイルのチェックボックスを更新
