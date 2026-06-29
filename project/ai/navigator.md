# Navigator

依頼内容から、AIが読むべき資料を判断するためのガイドです。

このファイルは「次に何を読むか」を決めるためだけに使います。仕様詳細や実装ルールは各リンク先にあります。

## 基本ルール

1. 作業状態が影響しそうなら、最初に [state.md](state.md) を読む
2. 機能が明確なら、該当する `features/` を読む
3. 作業種別が明確なら、該当する `skills/` を読む
4. 複数レイヤーにまたがるなら [architecture.md](architecture.md) を読む
5. UI判断が含まれるなら [design.md](design.md) を読む
6. コードを書く前に必要な範囲で [coding_rules.md](coding_rules.md) を読む

## 依頼別ルート

### UI変更

例: Todo一覧の見た目を変える、完了ボタンの配置を変える

読む順:

1. [state.md](state.md)
2. [design.md](design.md)
3. [skills/frontend.md](skills/frontend.md)
4. 該当する `features/*.md`

読まなくてよい可能性が高い資料:

- [skills/backend.md](skills/backend.md)
- [skills/graphql.md](skills/graphql.md)

### Reactコンポーネント修正

例: TodoItemのチェックボックス挙動を変える

読む順:

1. [skills/frontend.md](skills/frontend.md)
2. [features/todo.md](features/todo.md)
3. 必要なら [coding_rules.md](coding_rules.md)

### API変更

例: Todo更新APIに `priority` を追加する

読む順:

1. [state.md](state.md)
2. [features/todo.md](features/todo.md)
3. [skills/graphql.md](skills/graphql.md)
4. [skills/backend.md](skills/backend.md)
5. [architecture.md](architecture.md)

### DB変更

例: Todoに期限日を追加する、通知用のテーブルを追加する

読む順:

1. [state.md](state.md)
2. 関連する `features/*.md`
3. [skills/backend.md](skills/backend.md)
4. [architecture.md](architecture.md)
5. [skills/testing.md](skills/testing.md)

### 認証・権限変更

例: ログイン必須画面を増やす、ユーザーごとにTodoを分離する

読む順:

1. [features/auth.md](features/auth.md)
2. [architecture.md](architecture.md)
3. [skills/backend.md](skills/backend.md)
4. [skills/frontend.md](skills/frontend.md)
5. [skills/testing.md](skills/testing.md)

### 通知変更

例: 期限切れTodoを通知する、通知頻度を変える

読む順:

1. [features/notification.md](features/notification.md)
2. [features/todo.md](features/todo.md)
3. [skills/backend.md](skills/backend.md)
4. 必要なら [skills/frontend.md](skills/frontend.md)
5. [skills/testing.md](skills/testing.md)

### テスト追加・テスト失敗調査

例: E2Eが落ちている、Todo作成のUnit Testを追加する

読む順:

1. [state.md](state.md)
2. [skills/testing.md](skills/testing.md)
3. 関連する `features/*.md`
4. 必要なら該当する `skills/*.md`

### リファクタリング

例: Todo関連の状態管理を整理する、Resolverを分割する

読む順:

1. [state.md](state.md)
2. [architecture.md](architecture.md)
3. [design.md](design.md)
4. 関連する `features/*.md`
5. 関連する `skills/*.md`
6. [coding_rules.md](coding_rules.md)

## 依頼文からのキーワード対応

| 依頼文のキーワード | 優先して読む資料 |
| --- | --- |
| 画面、UI、見た目、ボタン、フォーム | `design.md`, `skills/frontend.md` |
| React、Hooks、component、props | `skills/frontend.md`, `coding_rules.md` |
| API、resolver、schema、query、mutation | `skills/graphql.md`, `skills/backend.md` |
| DB、migration、table、index | `skills/backend.md`, `architecture.md` |
| login、session、user、permission | `features/auth.md` |
| todo、task、完了、期限 | `features/todo.md` |
| 通知、reminder、deadline | `features/notification.md` |
| test、spec、E2E、CI | `skills/testing.md` |
| 今の状態、未完了、作業中 | `state.md` |

## 終了条件

次の状態になったら、追加資料を読む前に作業へ進んでよいです。

- 対象機能が特定できている
- 対象レイヤーが特定できている
- 変更時の注意点が把握できている
- テスト方針が把握できている

不安だから全資料を読む、という判断は避けてください。必要になった時点で追加で読んでください。

