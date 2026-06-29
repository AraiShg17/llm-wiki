# Feature: Auth

認証機能に関する仕様、関連画面、API、DB、注意事項です。

ログイン、ログアウト、ログインユーザー、権限制御に関係する依頼ではこのファイルを読んでください。

## 概要

メールアドレスとパスワードによるログインを想定します。

できること:

- ログイン
- ログアウト
- ログイン中ユーザーの取得
- 未ログインユーザーの保護ページアクセス制御

対象外:

- OAuth
- 多要素認証
- パスワードリセット
- 組織、チーム、ロール管理

## 関連画面

| 画面 | 内容 |
| --- | --- |
| `LoginPage` | ログインフォーム |
| `TodoListPage` | ログイン必須 |
| `NotificationPage` | ログイン必須 |

## API

Query:

```graphql
viewer: User
```

Mutation:

```graphql
login(input: LoginInput!): AuthPayload!
logout: Boolean!
```

## DB

想定テーブル:

```text
users
  id
  email
  password_hash
  created_at
```

制約:

- `email` は一意
- `password_hash` は平文を保存しない

## 業務ルール

- 未ログインでTodo APIを呼んだ場合はUnauthorized
- ログイン済みユーザーは自分のTodoだけ操作できる
- `viewer` は未ログイン時に `null` を返す
- セッション期限切れ時はログイン画面へ誘導する

## 注意事項

- フロントエンドだけの制御を権限チェックとして扱わない
- Resolverで必ずログイン状態を検証する
- Service層には `userId` を明示的に渡す
- 認証状態の取得中は画面を一瞬ログイン済み扱いにしない

## 関連資料

- 全体構成: [../architecture.md](../architecture.md)
- UI: [../skills/frontend.md](../skills/frontend.md)
- Backend: [../skills/backend.md](../skills/backend.md)
- GraphQL: [../skills/graphql.md](../skills/graphql.md)
- テスト: [../skills/testing.md](../skills/testing.md)

