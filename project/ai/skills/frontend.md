# Skill: Frontend

UI、React、状態管理、画面テストに関係する作業で読む資料です。

## 読む条件

読む:

- 画面変更
- コンポーネント修正
- フォーム挙動変更
- ローディング、エラー、空状態の変更
- GraphQL Query結果の表示変更

読まなくてよい:

- DBだけの変更
- Resolver内部だけの変更
- バッチ処理だけの変更

## 先に確認する資料

- UI判断がある場合: [../design.md](../design.md)
- Todo画面: [../features/todo.md](../features/todo.md)
- 認証導線: [../features/auth.md](../features/auth.md)
- 通知表示: [../features/notification.md](../features/notification.md)

## 修正対象の探し方

想定パス:

```text
src/features/todo/components/
src/features/todo/hooks/
src/features/auth/components/
src/features/notification/components/
src/shared/components/
```

優先して見る順:

1. Page component
2. Feature component
3. Custom hook
4. GraphQL query document
5. Shared component

Shared componentは最後に確認してください。Todo固有の変更をSharedに入れないためです。

## 実装時の確認事項

- ローディング状態があるか
- 空状態があるか
- エラー状態があるか
- 保存中に二重送信されないか
- キーボード操作で主要操作ができるか
- 認証状態の読み込み中に誤った画面が出ないか

## テスト方法

Unit / Component:

- フォーム入力
- ボタンクリック
- エラー表示
- 空状態表示

E2E:

- ログイン
- Todo作成
- Todo完了
- Todo削除

## AIへの注意

- UI修正だけでも、関連するGraphQL型が変わる場合は [graphql.md](graphql.md) を読んでください。
- コンポーネントを分割する前に、分割後の責務が明確か確認してください。
- `data-testid` を追加する前に、アクセシブルなroleやlabelで選択できないか確認してください。

