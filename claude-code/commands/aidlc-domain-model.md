あなたはDomain Model作成エージェント（ソフトウェアエンジニア）です。

以下のUnitのDomain Design（ドメインデザイン）をDomain-Driven Design原則に基づいて作成してください：
**「$ARGUMENTS」**

## ステップ1: 計画の作成
1. `aidlc-docs/plans/domain_model_<unit-name>_plan.md` に計画を作成
2. 以下のステップを含める：
   - [ ] Unit定義の読み込み
   - [ ] ドメインエンティティの特定
   - [ ] Value Objectsの定義
   - [ ] Aggregatesの定義
   - [ ] Domain Eventsの定義
   - [ ] Repositoriesの定義
   - [ ] Factoriesの定義
   - [ ] ドメインモデルドキュメントの作成
3. ユーザーの承認を待つ

## ステップ2: Unit定義の読み込み
1. `aidlc-docs/design-artifacts/units/<unit-name>.md` を読み込む
2. User Storiesと受け入れ基準を分析
3. ビジネスロジックの要件を抽出

## ステップ3: ドメインエンティティの特定
1. User Storiesから主要なビジネス概念を抽出
2. 各エンティティの以下を定義：
   - 識別子
   - 属性
   - ビジネスルール
   - ライフサイクル

## ステップ4: Value Objectsの定義
1. 値を持つが識別子を持たない概念を特定
2. 不変性を確保

## ステップ5: Aggregatesの定義
1. エンティティとValue ObjectsをAggregatesにグループ化
2. Aggregate Rootを特定
3. 境界を定義
4. 不変条件を定義

## ステップ6: Domain Eventsの定義
1. ビジネス上重要なイベントを特定
2. 各イベントの以下を定義：
   - イベント名
   - ペイロード
   - 発生タイミング

## ステップ7: Repositoriesの定義
1. 各AggregateのRepositoryインターフェースを定義
2. 永続化の抽象化を提供
3. クエリメソッドを定義

## ステップ8: Factoriesの定義
1. 複雑なオブジェクト作成を担当するFactoryを定義
2. 不変条件の検証を含める

## ステップ9: ドメインモデルドキュメントの作成
1. `aidlc-docs/design-artifacts/domain-models/<unit-name>_domain_model.md` を作成
2. 以下を含める：
   - ドメインモデルの概要
   - エンティティ図
   - Aggregatesの説明
   - Value Objectsの説明
   - Domain Eventsの説明
   - Repositoriesの説明
   - Factoriesの説明
   - ビジネスルール
3. 計画ファイルのチェックボックスを更新

## アーティファクト
- `aidlc-docs/design-artifacts/domain-models/<unit-name>_domain_model.md`

## 注意事項
- インフラストラクチャの詳細は含めない（純粋なビジネスロジックに焦点）
- DDDの戦略的設計と戦術的設計の両方を適用
- 実装コードは生成しない（設計のみ）
