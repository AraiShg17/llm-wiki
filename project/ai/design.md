# Design

このファイルは、UI、コンポーネント設計、状態管理、命名に関する判断が必要なときに読んでください。

APIやDBだけの変更では、通常読む必要はありません。

## 設計思想

Todoアプリは、短時間で入力し、状態を素早く把握するための作業ツールです。

優先する体験:

- 一覧のスキャン性
- 入力の速さ
- 完了、未完了、期限切れの判別しやすさ
- エラー時に次の行動が分かること

避けること:

- 装飾が多く、一覧密度を下げるUI
- 状態が見た目だけで判別されるUI
- モーダルを多用して流れを止めるUI

## UI設計

画面:

- `TodoListPage`: 一覧、フィルタ、追加フォームを表示
- `LoginPage`: メールアドレスとパスワードでログイン
- `NotificationPage`: 通知一覧と既読操作

Todo一覧:

- 未完了を上、完了済みを下に表示
- 期限切れは日付ラベルを強調
- 完了済みはタイトルを弱く表示
- 削除操作は誤操作防止の確認を入れる

フォーム:

- タイトルは必須
- タイトルは1行
- 説明は任意
- 期限日は任意
- 保存中は二重送信を防ぐ

## コンポーネント設計

コンポーネントは次の単位に分けます。

| 種別 | 例 | 役割 |
| --- | --- | --- |
| Page | `TodoListPage` | データ取得と画面全体の配置 |
| Feature Component | `TodoList`, `TodoForm` | 機能単位のUI |
| Item Component | `TodoItem` | 1データ単位の表示 |
| Shared Component | `Button`, `TextField` | 汎用UI |

原則:

- Page以外のコンポーネントはURLやルーティングを知らない
- Shared ComponentはTodo固有の文言を持たない
- Feature ComponentはDBカラム名ではなくドメイン名でpropsを受ける

## 状態管理

状態は近い場所に置きます。

| 状態 | 置き場所 |
| --- | --- |
| 入力中フォーム値 | `TodoForm` 内 |
| 一覧フィルタ | URL query または Page |
| GraphQL取得結果 | GraphQL client cache |
| ログインユーザー | Auth provider |
| トースト表示 | Shared notification provider |

グローバル状態にしてよいもの:

- ログインユーザー
- アプリ全体の通知
- テーマやロケール

グローバル状態にしないもの:

- TodoFormの入力値
- TodoItemのhover状態
- 一時的な確認ダイアログの開閉

## 命名規則

React:

- Component: `PascalCase`
- Hook: `useXxx`
- Event handler: `handleXxx`
- Boolean props: `isXxx`, `hasXxx`, `canXxx`

Todo関連:

- `Todo`: APIから返るTodo
- `TodoItem`: 表示コンポーネント
- `TodoInput`: フォーム入力値
- `TodoFilter`: 一覧の絞り込み条件

避ける名前:

- `data`
- `item`
- `info`
- `flag`
- `handleClick` のように意味が薄い名前

## AIへの注意

- UI変更では、見た目だけでなく状態、空状態、エラー、ロード中も確認してください。
- コンポーネント分割は増やしすぎないでください。再利用か責務分離の理由がある場合だけ分けます。
- Todo固有の知識を `shared/` に入れないでください。

