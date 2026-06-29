# Feature: Notification

通知機能に関する仕様、関連画面、API、DB、注意事項です。

期限切れTodo、通知一覧、既読処理に関係する依頼ではこのファイルを読んでください。

## 概要

未完了かつ期限切れのTodoについて、ユーザーへ通知します。

できること:

- 通知一覧を見る
- 未読通知数を見る
- 通知を既読にする
- 通知から対象Todoへ移動する

対象外:

- メール送信
- Push通知
- Slackなど外部連携
- 繰り返し通知

## 関連画面

| 画面 | 内容 |
| --- | --- |
| `NotificationPage` | 通知一覧 |
| `NotificationBadge` | 未読件数 |
| `TodoListPage` | 期限切れTodo表示 |

## API

Query:

```graphql
notifications: [Notification!]!
unreadNotificationCount: Int!
```

Mutation:

```graphql
markNotificationRead(id: ID!): Notification!
markAllNotificationsRead: Boolean!
```

## DB

想定テーブル:

```text
notifications
  id
  user_id
  todo_id
  type
  read_at
  created_at
```

制約:

- `user_id` は必須
- `todo_id` は期限切れTodo通知の場合に必須
- `type` は `todo_overdue` を想定

## 業務ルール

- 通知対象は、未完了かつ期限日が過去のTodo
- 同じTodoに対する未読の期限切れ通知は重複作成しない
- Todoが完了したら、関連する未読通知は既読扱いにする
- 通知はログインユーザー本人のものだけ表示する

## 未確定事項

- 通知生成をバッチで行うか、一覧取得時に生成するか
- 期限日のタイムゾーン基準
- 通知の保持期間

## 注意事項

- Todoの `due_date` と密接に関係するため、Todo仕様変更時にも確認する
- 通知の重複作成を防ぐDB制約またはServiceロジックが必要
- 期限判定は日付境界でテストする

## 関連資料

- Todo仕様: [todo.md](todo.md)
- Backend: [../skills/backend.md](../skills/backend.md)
- GraphQL: [../skills/graphql.md](../skills/graphql.md)
- UI: [../skills/frontend.md](../skills/frontend.md)
- テスト: [../skills/testing.md](../skills/testing.md)

