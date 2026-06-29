# AI Index

このファイルはAIエージェントが最初に読む入口です。

目的は、このプロジェクトの全体像を短く把握し、次に読むべき資料を選ぶことです。ここに詳細な設計や規約は書きません。

## プロジェクト概要

小規模なTodoアプリです。

想定機能:

- Todoの作成、更新、完了、削除
- ユーザー認証
- 期限切れTodoの通知

想定技術:

- Frontend: React + TypeScript
- Backend: Node.js + GraphQL
- Database: PostgreSQL
- Testing: Unit / Integration / E2E

## 最初の判断

依頼を受けたら、次の順で確認してください。

1. 現在の作業状況を確認する必要がある場合は [state.md](state.md)
2. どの資料を読むべきか迷う場合は [navigator.md](navigator.md)
3. UI、API、DB、テストなど作業種別が明確な場合は `skills/` の該当ファイル
4. Todo、認証、通知など機能が明確な場合は `features/` の該当ファイル
5. システム全体の構造が必要な場合だけ [architecture.md](architecture.md)
6. 設計思想やUI方針が必要な場合だけ [design.md](design.md)
7. 実装ルールが必要な場合だけ [coding_rules.md](coding_rules.md)

## ドキュメント一覧

| ファイル | 役割 | 読む条件 |
| --- | --- | --- |
| [navigator.md](navigator.md) | 依頼内容から読む資料を決める | どこを読めばよいか不明なとき |
| [state.md](state.md) | 現在の作業状況 | 作業開始時、既存作業の影響を確認したいとき |
| [architecture.md](architecture.md) | システム構成 | 複数レイヤーにまたがる変更時 |
| [design.md](design.md) | UI、状態管理、設計思想 | 画面やコンポーネントの変更時 |
| [coding_rules.md](coding_rules.md) | 実装ルール | コード生成、修正、レビュー時 |
| [features/todo.md](features/todo.md) | Todo機能 | Todoの仕様変更時 |
| [features/auth.md](features/auth.md) | 認証機能 | ログイン、セッション、権限制御の変更時 |
| [features/notification.md](features/notification.md) | 通知機能 | 通知、期限、リマインダーの変更時 |
| [skills/frontend.md](skills/frontend.md) | フロントエンド作業知識 | UI、React、状態管理、画面テストの変更時 |
| [skills/backend.md](skills/backend.md) | バックエンド作業知識 | API、DB、ドメインロジックの変更時 |
| [skills/graphql.md](skills/graphql.md) | GraphQL作業知識 | Schema、Resolver、Query、Mutationの変更時 |
| [skills/testing.md](skills/testing.md) | テスト作業知識 | テスト追加、修正、失敗調査時 |
| [consideration.md](consideration.md) | LLM Wikiとしての考察 | 構成評価、改善検討時 |

## 読まない判断も重要

次のような場合は、全資料を読む必要はありません。

- ボタン文言だけの変更: `design.md` と `skills/frontend.md` の必要箇所だけ読む
- GraphQLの型追加だけ: `skills/graphql.md` と該当 `features/*.md` だけ読む
- テスト失敗の調査だけ: `skills/testing.md` と関連機能だけ読む
- 進行中作業の衝突確認だけ: `state.md` だけ読む

## AIへの注意

- READMEを作業判断の中心にしないでください。
- 不明点がある場合でも、まず [navigator.md](navigator.md) で読む範囲を絞ってください。
- `state.md` は最新状態の要約であり、恒久的な仕様ではありません。
- `features/` は機能仕様、`skills/` は作業方法です。混同しないでください。

