# Skill: Backend

API、Service、Repository、DBに関係する作業で読む資料です。

## 読む条件

読む:

- Resolver修正
- Service修正
- DB schema変更
- 業務ルール変更
- 認証、権限チェック変更
- 通知生成ロジック変更

読まなくてよい:

- CSSだけの変更
- 文言だけの変更
- UIコンポーネントの表示順だけの変更

## 先に確認する資料

- Todo仕様: [../features/todo.md](../features/todo.md)
- 認証仕様: [../features/auth.md](../features/auth.md)
- 通知仕様: [../features/notification.md](../features/notification.md)
- 全体構成: [../architecture.md](../architecture.md)

## 修正対象の探し方

想定パス:

```text
src/server/resolvers/
src/server/services/
src/server/repositories/
src/server/db/
src/server/schema/
```

優先して見る順:

1. GraphQL schema
2. Resolver
3. Service
4. Repository
5. DB migration
6. Tests

## 実装時の確認事項

- Resolverで認証チェックをしているか
- Serviceに `userId` が明示的に渡っているか
- Repositoryがログイン状態を暗黙参照していないか
- DB制約とServiceのバリデーションが矛盾していないか
- エラーがUIで扱える粒度になっているか

## DB変更時

確認すること:

- 既存データへのデフォルト値
- nullable / not null
- index
- unique制約
- rollback方針
- テストデータ更新

Todoで特に注意:

- `due_date` はタイムゾーン境界の影響を受ける
- `priority` は許容値をGraphQL、Service、DBで揃える
- `user_id` 条件漏れは重大なデータ漏洩につながる

## テスト方法

- Service unit testで業務ルールを検証
- Resolver integration testで認証とGraphQL契約を検証
- Repository testでDB制約とクエリ条件を検証

## AIへの注意

- API変更をした場合は [graphql.md](graphql.md) も読んでください。
- DB変更だけで終わらせず、関連するService、GraphQL、テストへの影響を確認してください。
- 認証に関係する変更では、必ず他ユーザーのデータにアクセスできないことを確認してください。

