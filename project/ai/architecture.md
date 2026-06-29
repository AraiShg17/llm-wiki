# Architecture

このファイルは、システム全体の構造を把握する必要があるときだけ読んでください。

単一コンポーネントの見た目変更や小さな文言変更では、通常読む必要はありません。

## 想定ディレクトリ

実装コードがある場合は、次の構成を想定します。

```text
src/
  app/
    routes/
    providers/
  features/
    todo/
      components/
      hooks/
      graphql/
      tests/
    auth/
    notification/
  shared/
    components/
    graphql/
    utils/
    errors/
  server/
    schema/
    resolvers/
    services/
    repositories/
    db/
```

## レイヤー

| レイヤー | 責務 | 依存してよい対象 |
| --- | --- | --- |
| UI Component | 表示とユーザー操作 | hooks, shared components |
| Feature Hook | 画面用状態、GraphQL呼び出し | generated GraphQL hooks, utils |
| GraphQL Schema | API契約 | domain input/output |
| Resolver | 認証、入力検証、Service呼び出し | services |
| Service | 業務ルール | repositories |
| Repository | DBアクセス | db client |
| DB | 永続化 | なし |

## 依存方向

```text
UI -> Hook -> GraphQL Client -> Resolver -> Service -> Repository -> DB
```

逆方向の依存は禁止です。

例:

- RepositoryがServiceを呼ばない
- ServiceがReactの型を参照しない
- UIがDBのカラム名に直接依存しない

## コンポーネント責務

| コンポーネント | 責務 | 持たない責務 |
| --- | --- | --- |
| `TodoList` | Todo配列の表示、空状態表示 | API呼び出し、DB知識 |
| `TodoItem` | 1件の表示、完了切替操作 | 一覧取得、認証判断 |
| `TodoForm` | 入力、バリデーション表示 | 永続化処理の詳細 |
| `AuthGuard` | 未ログイン時の導線制御 | Todo仕様 |
| `NotificationBadge` | 未読通知数の表示 | 通知抽出ロジック |

## API構成

GraphQLを想定します。

主要Query:

- `viewer`: ログイン中ユーザーを返す
- `todos(filter: TodoFilter): [Todo!]!`: Todo一覧を返す
- `notifications: [Notification!]!`: 通知一覧を返す

主要Mutation:

- `createTodo(input: CreateTodoInput!): Todo!`
- `updateTodo(input: UpdateTodoInput!): Todo!`
- `completeTodo(id: ID!): Todo!`
- `deleteTodo(id: ID!): DeleteResult!`
- `login(input: LoginInput!): AuthPayload!`
- `logout: Boolean!`
- `markNotificationRead(id: ID!): Notification!`

## データモデル

主要テーブル:

```text
users
  id
  email
  password_hash
  created_at

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

notifications
  id
  user_id
  todo_id
  type
  read_at
  created_at
```

## クロスカット関心事

認証:

- Resolverでユーザーを確定する
- Service以下には `userId` を明示的に渡す
- Repositoryで暗黙のログイン状態を参照しない

エラー:

- 入力エラーはGraphQLのUserInputError相当
- 権限エラーはUnauthorizedまたはForbidden
- 想定外エラーは詳細をクライアントへ返さない

テスト:

- UIはユーザー操作ベース
- Serviceは業務ルールベース
- Resolverは認証と入出力契約ベース
- E2Eは主要ユーザーフローだけ

