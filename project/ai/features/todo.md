# Feature: Todo

Todo機能に関する仕様、関連画面、API、DB、注意事項です。

Todoの作成、更新、完了、削除、一覧表示に関係する依頼ではこのファイルを読んでください。

## 概要

ユーザーは自分のTodoを管理できます。

できること:

- Todoを作成する
- Todo一覧を見る
- Todoを完了にする
- Todoを編集する
- Todoを削除する
- 未完了、完了済み、期限切れで絞り込む

対象外:

- 他ユーザーとの共有
- サブタスク
- 添付ファイル
- 繰り返しTodo

## 関連画面

| 画面 | 内容 |
| --- | --- |
| `TodoListPage` | Todo一覧、追加フォーム、フィルタ |
| `TodoDetailPanel` | Todoの詳細編集 |
| `NotificationPage` | 期限切れTodoへの導線 |

## API

Query:

```graphql
todos(filter: TodoFilter): [Todo!]!
```

Mutation:

```graphql
createTodo(input: CreateTodoInput!): Todo!
updateTodo(input: UpdateTodoInput!): Todo!
completeTodo(id: ID!): Todo!
deleteTodo(id: ID!): DeleteResult!
```

## DB

想定テーブル:

```text
todos
  id
  user_id
  title
  description
  completed
  due_date
  priority
  created_at
  updated_at
```

制約:

- `title` は必須
- `user_id` は必須
- `completed` はデフォルト `false`
- `priority` は `low`, `normal`, `high` のいずれか

## 業務ルール

- ログインユーザーは自分のTodoだけ操作できる
- 完了済みTodoも削除できる
- 削除は論理削除ではなく物理削除を想定
- 期限日が今日より前で未完了の場合、期限切れとして扱う
- Todo作成時の初期priorityは `normal`

## 注意事項

- Todo一覧の表示順は、未完了、期限日が近い順、作成日の新しい順
- 期限切れ判定はバックエンドとフロントエンドでずれやすい
- ユーザーのタイムゾーンを考慮する必要がある
- 通知機能は `due_date` に依存する

## 関連資料

- UI変更: [../design.md](../design.md), [../skills/frontend.md](../skills/frontend.md)
- API変更: [../skills/graphql.md](../skills/graphql.md), [../skills/backend.md](../skills/backend.md)
- テスト: [../skills/testing.md](../skills/testing.md)
- 通知との関係: [notification.md](notification.md)

