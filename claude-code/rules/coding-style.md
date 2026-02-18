---
paths:
  - "**/*.ts"
  - "**/*.tsx"
  - "**/*.js"
  - "**/*.jsx"
  - "**/*.py"
  - "**/*.go"
---

# コーディングスタイル

## イミュータビリティ（重要）

**常に新しいオブジェクトを作成し、決して変更しない**:

```javascript
// ❌ 悪い例: 変更
function updateUser(user, name) {
  user.name = name  // 変更！
  return user
}

// ✅ 良い例: イミュータビリティ
function updateUser(user, name) {
  return {
    ...user,
    name
  }
}
```

## ファイル構成

**多くの小さなファイル > 少数の大きなファイル**:
- 高凝集度、低結合度
- 200-400行が典型的、最大800行
- 大きなコンポーネントからユーティリティを抽出
- 型ではなく機能/ドメインで整理

## エラーハンドリング

**常に包括的なエラーハンドリングを実装**:

```typescript
try {
  const result = await riskyOperation()
  return result
} catch (error) {
  console.error('Operation failed:', error)
  throw new Error('詳細なユーザーフレンドリーなメッセージ')
}
```

## 入力検証

**常にユーザー入力を検証**:

```typescript
import { z } from 'zod'

const schema = z.object({
  email: z.string().email(),
  age: z.number().int().min(0).max(150)
})

const validated = schema.parse(input)
```

## コード品質チェックリスト

作業完了前に確認:
- [ ] コードが読みやすく、適切に命名されている
- [ ] 関数が小さい（<50行）
- [ ] ファイルが焦点を絞っている（<800行）
- [ ] 深いネストがない（>4レベル）
- [ ] 適切なエラーハンドリング
- [ ] console.logステートメントがない
- [ ] ハードコードされた値がない
- [ ] 変更がない（イミュータブルパターンを使用）

## AI-DLC統合

- **Code Generationコマンド**: 生成されたコードがこのスタイルガイドに準拠していることを確認
- **コードレビュー**: すべてのコード生成後に自動的にスタイルチェックを実行
