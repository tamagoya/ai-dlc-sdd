# Everything Claude Code テクニック統合提案

## 概要

`affaan-m/everything-claude-code`リポジトリで公開されている実践的なテクニックを、AI-DLCフレームワークに統合する提案です。

## 分析結果

### 現在のAI-DLCフレームワークの構造

```
ai-dlc-sdd/
├── cursor/
│   ├── AGENTS.md          # 専門家の役割定義（Commands内に統合済み）
│   ├── agents/            # （廃止）エージェント定義はCommands内に統合
│   └── commands/          # AI-DLCコマンド（専門家の役割を含む）
│       ├── aidlc-setup.md
│       ├── aidlc-inception.md
│       ├── aidlc-domain-model.md
│       ├── aidlc-code-generation.md
│       └── ...
└── docs/
    ├── AI-DLC.md
    └── PROJECT_STRUCTURE.md
```

### Everything Claude Codeの主要テクニック

1. **専門家の役割（Commands内に統合）**: 特定タスクに特化した専門家の役割（Cursor公式ドキュメントのベストプラクティスに基づき、Commands内で実装）
2. **Rules（ルール）**: 常に従うべきガイドライン
3. **Skills（スキル）**: ワークフロー定義とドメイン知識
4. **Commands（コマンド）**: スラッシュコマンド
5. **Hooks（フック）**: ツール使用時の自動化
6. **Performance最適化**: モデル選択、コンテキスト管理
7. **並列タスク実行**: 独立操作の並列実行

## 統合提案

### 1. Rules（ルール）の追加

**目的**: コード品質、セキュリティ、テスト、パフォーマンスの一貫性を保つ

**提案するルールファイル**:

```
cursor/rules/
├── security.md          # セキュリティガイドライン
├── coding-style.md      # コーディングスタイル
├── testing.md          # テスト要件（80%カバレッジ、TDD）
├── performance.md       # パフォーマンス最適化（モデル選択、コンテキスト管理）
├── git-workflow.md      # Gitワークフロー
└── agents.md            # エージェント使用ガイドライン
```

**優先度**: 高
**理由**: AI-DLCのコード生成フェーズで品質を保証するため

### 2. Skills（スキル）の追加

**目的**: ドメイン知識とベストプラクティスを共有

**提案するスキルファイル**:

```
cursor/skills/
├── backend-patterns.md      # バックエンドパターン（API、DB、キャッシュ）
├── frontend-patterns.md      # フロントエンドパターン（React、Next.js）
├── ddd-patterns.md          # DDDパターン（AI-DLC固有）
├── tdd-workflow/            # TDDワークフロー
│   ├── README.md
│   └── workflow.md
└── security-review/         # セキュリティレビューチェックリスト
    ├── README.md
    └── checklist.md
```

**優先度**: 中
**理由**: AI-DLCのConstruction Phaseでパターンを適用するため

### 3. 専門家の役割の追加（Commands内に統合）✅ 完了

**目的**: 特定タスクに特化した専門家の役割で品質向上

**実装状況**: Cursor公式ドキュメントのベストプラクティスに基づき、エージェントを廃止し、Commands内で専門家の役割として実装しました。

**実装された専門家の役割**:

```
Commands内に統合:
├── 計画スペシャリスト      # aidlc-inceptionコマンド内（ステップ1）
├── アーキテクト            # aidlc-architectureコマンド内（ステップ1, 3, 5, 6）
├── コードレビュー専門家    # aidlc-code-generation（ステップ10）、aidlc-code-review
├── セキュリティ専門家      # aidlc-code-generation（ステップ11）、aidlc-security-review
├── TDD専門家               # aidlc-code-generationコマンド内（ステップ7）
└── ビルドエラー解決専門家  # aidlc-code-generation（ステップ9）、aidlc-build-fix
```

**優先度**: 高 ✅ 完了
**理由**: AI-DLCの各フェーズで品質を保証するため

### 4. Hooks（フック）の追加

**目的**: 自動化による品質向上と開発効率化

**提案するフック**:

```json
cursor/hooks/hooks.json
```

**主要なフック**:
- PreToolUse: 開発サーバーをtmuxで実行するよう促す
- PostToolUse: コード編集後の自動フォーマット、TypeScriptチェック
- Stop: セッション終了時のconsole.log検出

**優先度**: 中
**理由**: 開発体験の向上

### 5. コマンドの拡張

**目的**: 既存のAI-DLCコマンドを拡張

**提案する追加コマンド**:

```
cursor/commands/
├── aidlc-code-review.md    # コードレビュー（/aidlc-code-review）
├── aidlc-security-review.md # セキュリティレビュー（/aidlc-security-review）
└── aidlc-build-fix.md      # ビルドエラー修正（/aidlc-build-fix）
```

**優先度**: 中
**理由**: 既存コマンドの補完

### 6. Performance最適化の統合

**目的**: コンテキストウィンドウとモデル選択の最適化

**提案**:
- `cursor/rules/performance.md`に以下を追加:
  - モデル選択戦略（Haiku/Sonnet/Opus）
  - コンテキストウィンドウ管理
  - 並列タスク実行ガイドライン

**優先度**: 高
**理由**: コストとパフォーマンスの最適化

## 実装計画

### Phase 1: 基盤の構築（優先度: 高）

1. **Rulesの追加**
   - `cursor/rules/security.md`
   - `cursor/rules/testing.md`
   - `cursor/rules/performance.md`
   - `cursor/rules/coding-style.md`

2. **Performance最適化の統合**
   - `cursor/rules/performance.md`にモデル選択戦略を追加
   - `cursor/AGENTS.md`にモデル指定を追加

### Phase 2: 専門家の役割の追加（優先度: 高）✅ 完了

**注意**: Cursor公式ドキュメントのベストプラクティスに基づき、エージェントを廃止し、Commands内で専門家の役割として実装しました。

1. **コードレビュー専門家**
   - `aidlc-code-generation`コマンド内に統合（ステップ10）
   - `aidlc-code-review`コマンド内に実装

2. **セキュリティ専門家**
   - `aidlc-code-generation`コマンド内に統合（ステップ11）
   - `aidlc-security-review`コマンド内に実装

3. **TDD専門家**
   - `aidlc-code-generation`コマンド内に統合（ステップ7）

4. **ビルドエラー解決専門家**
   - `aidlc-code-generation`コマンド内に統合（ステップ9）
   - `aidlc-build-fix`コマンド内に実装

5. **計画スペシャリスト**
   - `aidlc-inception`コマンド内に統合（ステップ1）

6. **アーキテクト**
   - `aidlc-architecture`コマンド内に統合（ステップ1, 3, 5, 6）

### Phase 3: Skillsの追加（優先度: 中）

1. **バックエンドパターン**
   - `cursor/skills/backend-patterns.md`

2. **TDDワークフロー**
   - `cursor/skills/tdd-workflow/`

3. **セキュリティレビュー**
   - `cursor/skills/security-review/`

### Phase 4: Hooksとコマンドの追加（優先度: 中）

1. **Hooksの追加**
   - `cursor/hooks/hooks.json`

2. **追加コマンド**
   - `aidlc-code-review.md`
   - `aidlc-security-review.md`

## 統合のメリット

1. **品質向上**
   - 自動化されたセキュリティチェック
   - 80%テストカバレッジの強制
   - コードレビューの自動化

2. **開発効率化**
   - 並列タスク実行
   - 自動フォーマットとリント
   - ビルドエラーの自動解決

3. **コスト最適化**
   - モデル選択戦略によるコスト削減
   - コンテキストウィンドウの最適化

4. **一貫性の確保**
   - 統一されたコーディングスタイル
   - 標準化されたワークフロー

## 注意事項

1. **AI-DLCフレームワークとの整合性**
   - 既存のAI-DLCコマンドとの統合を優先
   - 新しい概念を追加する際は、AI-DLCの原則と整合性を保つ

2. **段階的な導入**
   - 一度にすべてを導入せず、Phaseごとに実装
   - 各Phaseで効果を検証

3. **カスタマイズ**
   - プロジェクト固有の要件に合わせて調整
   - 不要な機能は削除

## 次のステップ

1. この提案をレビュー
2. Phase 1から実装を開始
3. 各Phaseで効果を測定
4. フィードバックに基づいて調整

## Cursor公式ドキュメント準拠

この統合は、Cursor公式ドキュメントのベストプラクティスに準拠しています：

- **Rules**: `.mdc` 形式（Markdown with frontmatter）を使用
- **Commands**: `.md` 形式（プレーンマークダウン）を使用
- **Agents**: `.md` 形式（YAML frontmatter付き）を使用

詳細は [Cursor準拠チェックドキュメント](CURSOR_COMPLIANCE_CHECK.md) を参照してください。

## 参考資料

- [Everything Claude Code](https://github.com/affaan-m/everything-claude-code)
- [The Shorthand Guide to Everything Claude Code](https://x.com/affaanmustafa/status/2012378465664745795)
- [Cursor Rules Documentation](https://docs.cursor.com/context/rules)
- [Cursor Commands Documentation](https://docs.cursor.com/en/agent/chat/commands)
