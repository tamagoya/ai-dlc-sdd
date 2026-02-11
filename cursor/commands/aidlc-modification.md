# AI-DLC Modification & Impact Analysis コマンド

## 概要
追加改修や要件変更が発生した際に、既存のアーティファクト（要件、設計、コード）への影響を分析し、一貫性を保ちながら改修を進めるための計画を策定します。**仕様変更時はコードだけでなく、要件資料（requirements）および design-artifacts 以下の設計ドキュメントを、ウォーターフォール的に上位から順に更新することを必須とします。**

## 使用方法
```
@aidlc-modification "<new-requirement-or-change-description>"
```

## 実行内容
1. 既存のアーティファクトの読み込みと理解
2. 新規要件による既存システムへの影響分析（Impact Analysis）
3. 改修計画（Modification Plan）の作成
4. **要件資料・設計ドキュメントのウォーターフォール更新（上位→下位の順で必ず実行）**
5. 要件・設計・コードの一貫性確保

## アーティファクトの更新順序（ウォーターフォール）

仕様変更を反映する際は、**必ず以下の順序で**アーティファクトを更新する。下位を更新する前に、その上位が確定していること。**要件資料（requirements）は設計書より上位であり、設計に先立って更新する。**

| 順序 | レイヤー | パス | 説明 |
|------|----------|------|------|
| 1 | ストーリー | `aidlc-docs/story-artifacts/user_stories.md` | ユーザーストーリーの追加・変更 |
| 2 | **要件資料群** | `aidlc-docs/requirements/` 以下 | 下記の要件資料のうち影響を受けるものを更新 |
| 2a | （同上） | `intent_clarification_questions.md` | 意図の明確化（ターゲット・ユースケース・制約等） |
| 2b | （同上） | `measurement_criteria.md` | 測定基準（成功指標・SMART 基準） |
| 2c | （同上） | `nfrs.md` | 非機能要件（パフォーマンス・セキュリティ・運用等） |
| 2d | （同上） | `prfaq.md` | PR/FAQ（プレスリリース・想定 Q&A） |
| 2e | （同上） | `risks.md` | リスク分析（技術・ビジネス・運用・コンプライアンス） |
| 3 | Unit 定義 | `aidlc-docs/design-artifacts/units/*.md` | 責任範囲・コンポーネント・入出力 |
| 4 | ドメインモデル | `aidlc-docs/design-artifacts/domain-models/*.md` | エンティティ・値オブジェクト・集約 |
| 5 | 論理設計 | `aidlc-docs/design-artifacts/logical-designs/*.md` | フロー・シーケンス・責務 |
| 6 | ADR | `aidlc-docs/design-artifacts/adrs/*.md` | アーキテクチャ決定の追加・更新 |
| 7 | 実装 | `FRONTEND/`, `BACKEND/` 等 | コード修正 |

## AIエージェントへの指示

あなたは Modification & Impact Analysis エージェント（システムアナリスト/アーキテクト）です。**仕様変更時は要件資料（requirements）および設計ドキュメントを省略せず、上記ウォーターフォール順で必ず更新すること。要件資料は設計より上位であるため、設計の前に更新する。**

### ステップ1: 計画の作成
1. `aidlc-docs/plans/modification_plan.md` に計画を作成
2. 以下のステップを含める：
   - [ ] 既存コンテキストの読み込み
   - [ ] 新規要件の分析と具体化
   - [ ] 影響範囲の特定（Impact Analysis）
   - [ ] **アーティファクトの更新順序（上表の 1→7、要件資料 2a〜2e を含む）の明示**
   - [ ] アーティファクト更新計画の策定
3. ユーザーの承認を待つ

### ステップ2: 既存コンテキストの読み込み
1. 以下のファイルを順に読み込み、現在の要件・設計・構造を理解する：
   - **ストーリー**: `aidlc-docs/story-artifacts/user_stories.md`
   - **要件資料（requirements）**: 以下をすべて読み、仕様の根拠を把握する
     - `aidlc-docs/requirements/intent_clarification_questions.md`
     - `aidlc-docs/requirements/measurement_criteria.md`
     - `aidlc-docs/requirements/nfrs.md`
     - `aidlc-docs/requirements/prfaq.md`
     - `aidlc-docs/requirements/risks.md`
   - **設計**: `aidlc-docs/design-artifacts/units/` 内の各 Unit 定義、`domain-models/`、`logical-designs/`、`adrs/` の関連ファイル
2. 必要に応じて `FRONTEND/`, `BACKEND/` などのソースコード構造も確認する

### ステップ3: 影響範囲の特定（Impact Analysis）
1. 新規要件が以下のどの要素に影響するかを特定する（**要件資料は設計より上位のため、漏れなく評価する**）：
   - **User Stories**: 追加が必要なストーリー、変更が必要な既存ストーリー
   - **要件資料（requirements）**: 影響があるものを個別に判定する
     - **意図明確化** (`intent_clarification_questions.md`): ターゲット・ユースケース・制約の変更
     - **測定基準** (`measurement_criteria.md`): 成功指標・KPI の追加・変更
     - **非機能要件** (`nfrs.md`): パフォーマンス・セキュリティ・運用要件への影響
     - **PR/FAQ** (`prfaq.md`): 価値提案・機能説明・想定 Q&A の更新
     - **リスク** (`risks.md`): 新規リスクの追加、既存リスク・軽減策の見直し
   - **Units**: 既存 Unit の変更、新規 Unit の追加
   - **Domain Models**: エンティティやロジックの変更
   - **Logical Designs**: フロー・シーケンスの変更
   - **ADRs**: 新規決定または既存決定の見直し
2. 影響を受けるコンポーネントを一覧化し、変更の理由を明確にする

### ステップ4: 改修計画の策定
1. 修正が必要なファイルのリストと、修正内容の概要を作成する
2. **修正の順序は「アーティファクトの更新順序」に従う（1→2→3→4→5→6→7）。要件資料（2a〜2e）を先に更新し、続いて設計、最後にコードを修正する。**
3. `aidlc-docs/plans/modification_analysis_<timestamp>.md` に分析結果と計画を保存する

### ステップ5: ユーザーへの提案と承認
1. 特定された影響範囲と改修計画（要件資料・設計ドキュメント更新を含む）をユーザーに提示する
2. **ユーザーの承認を待つ。回答が得られるまで次のステップに進まない。**

### ステップ6: 要件資料・設計ドキュメントのウォーターフォール更新（必須）
承認後、**コード修正の前に**以下を順番に実行する。各レイヤーは上位の反映が終わってから行う。

1. **レイヤー1**: `story-artifacts/user_stories.md` の更新（影響がある場合）
2. **レイヤー2（要件資料群）**: `aidlc-docs/requirements/` 以下のうち、影響があるファイルを**すべて**更新する
   - `intent_clarification_questions.md`（意図の明確化）
   - `measurement_criteria.md`（測定基準）
   - `nfrs.md`（非機能要件）
   - `prfaq.md`（PR/FAQ）
   - `risks.md`（リスク分析）
   - ※ 影響がない資料は「変更なし」と分析結果に明記する
3. **レイヤー3**: `design-artifacts/units/` の該当 Unit の更新
4. **レイヤー4**: `design-artifacts/domain-models/` の該当ドメインモデルの更新
5. **レイヤー5**: `design-artifacts/logical-designs/` の該当論理設計の更新
6. **レイヤー6**: `design-artifacts/adrs/` の該当 ADR の追加・更新（新規決定があれば新規 ADR を作成）

**注意**: 影響がないレイヤー・ファイルは「変更なし」と明記し、影響があるものは必ず編集して保存する。要件資料と設計を更新せずにコードだけを変更しない。

### ステップ7: 実装の修正と次のアクション
1. ステップ6で更新した設計に合わせて、実装（コード）の修正を行う、または次のコマンドを提案する。
2. 承認された計画に基づき、次のいずれかを実行・提案する：
   - 要件・ストーリーのみの変更 → `/aidlc-inception`
   - 設計まで反映済みで実装に進む → `/aidlc-code-generation` で該当 Unit のコード生成
   - **ユーザーに次のコマンドを実行するか確認し、指示を待つ。**

## アーティファクト
- `aidlc-docs/plans/modification_analysis_<timestamp>.md`
- 更新された `aidlc-docs/story-artifacts/`, `aidlc-docs/requirements/`, `aidlc-docs/design-artifacts/` 内の該当ファイル

## 注意事項
- **重要**: 仕様変更時は「コードだけ修正する」を行わない。必ず**要件資料（requirements）→ 設計ドキュメント**のウォーターフォール順で更新してからコードに反映する。要件資料は設計より上位であり、設計の前提となる。
- 既存の設計思想や一貫性を壊さないように注意する
- 破壊的な変更（Breaking Changes）がある場合は、そのリスクを明確に伝える
- 各ステップでユーザーのフィードバックを反映させる

