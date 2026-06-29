# Coding Rules

このファイルは、AIがコードを生成、修正、レビューするときに読む規約です。

実装コードはこのサンプルにはありませんが、実装がある場合は次の規約を適用します。

## TypeScript

- `any` は原則禁止
- APIレスポンス型はGraphQL generated typesを優先
- UI内部の一時的な型はコンポーネント近くに置く
- 共有型にするのは複数機能で使う場合だけ
- nullableとoptionalを混同しない

例:

```ts
type TodoFormValues = {
  title: string;
  description?: string;
  dueDate?: string;
};
```

## React Hooks

- Hooksはコンポーネントの先頭で呼ぶ
- 条件分岐の中でHooksを呼ばない
- `useEffect` は外部同期が必要な場合だけ使う
- 派生値は可能なら `useMemo` より通常の変数で表現する
- カスタムHookはUI表示ではなく状態と操作を返す

## Import順

```text
1. React / framework
2. external libraries
3. shared modules
4. feature modules
5. relative imports
6. styles
```

同じグループ内はアルファベット順にします。

## Error Handling

UI:

- ユーザーが修正できるエラーは画面に表示する
- 想定外エラーは汎用メッセージにする
- ログには調査可能な情報を残す

Backend:

- 入力値の不正はValidation Error
- 未ログインはUnauthorized
- 権限不足はForbidden
- DB制約違反はService層で意味のあるエラーに変換する

## GraphQL

- Mutation inputは必ずInput Objectにする
- QueryのfilterもInput Objectにする
- Resolverで認証を確認する
- ServiceにGraphQL固有のContextを渡さない
- Schema変更時は関連するUI、Service、テストを確認する

## テスト

- UIテストは実装詳細ではなくユーザー操作を検証する
- Serviceテストは業務ルールを直接検証する
- Resolverテストは認証、入力、返却型を検証する
- E2Eは主要導線だけに絞る

## コメント

コメントを書く条件:

- なぜその実装なのかがコードだけでは分からない
- 外部仕様や暫定対応がある
- 一見不要に見える処理に理由がある

書かないコメント:

- コードをそのまま説明するコメント
- 古い仕様のメモ
- TODOだけで担当や条件がないコメント

## AIへの注意

- 既存パターンがある場合は、この規約より既存パターンを優先してください。
- 規約違反を直すためだけの大規模リファクタリングはしないでください。
- 依頼範囲外の整形差分を増やさないでください。

