# Skill: GraphQL

GraphQL Schema、Query、Mutation、Resolver、generated typesに関係する作業で読む資料です。

## 読む条件

読む:

- Schema変更
- Query追加、変更
- Mutation追加、変更
- Resolver修正
- GraphQL generated typesの変更
- UIが取得するフィールド変更

読まなくてよい:

- DB内部だけの変更でAPI契約が変わらない場合
- CSSや文言だけの変更

## Schema方針

MutationはInput Objectを使います。

```graphql
input CreateTodoInput {
  title: String!
  description: String
  dueDate: Date
  priority: TodoPriority
}
```

戻り値は、単純な成功可否だけでなく、UIが更新に使うオブジェクトを返します。

```graphql
type Mutation {
  createTodo(input: CreateTodoInput!): Todo!
}
```

## 命名

| 種別 | 例 |
| --- | --- |
| Object | `Todo` |
| Input | `CreateTodoInput` |
| Filter | `TodoFilter` |
| Enum | `TodoPriority` |
| Payload | `AuthPayload` |

避ける名前:

- `TodoArgs`
- `TodoParams`
- `CommonInput`
- `Result`

## Resolver方針

Resolverの責務:

- 認証状態の確認
- 入力値の基本検証
- Service呼び出し
- GraphQL型への変換

Resolverに置かない責務:

- 複雑な業務ルール
- DBクエリの組み立て
- UI都合の整形

## UI影響確認

Schemaを変更したら確認すること:

- 使用中のQuery / Mutation
- generated types
- GraphQL mock
- Component props
- E2Eのfixture

## 後方互換性

小規模プロジェクトでも、既存UIを壊さない変更を優先します。

- フィールド削除より非推奨化を検討する
- 必須Input追加は既存呼び出しを壊す
- nullable変更はUIの分岐を増やす
- enum追加は表示ラベルが必要

## 関連資料

- Backend作業: [backend.md](backend.md)
- Frontend影響: [frontend.md](frontend.md)
- Todo仕様: [../features/todo.md](../features/todo.md)
- 認証仕様: [../features/auth.md](../features/auth.md)
- 通知仕様: [../features/notification.md](../features/notification.md)

