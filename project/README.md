# LLM Wiki Sample Project

Todoアプリを題材にした、AIエージェント向けドキュメント構成のサンプルです。

このプロジェクトには実装コードを置きません。目的は、Claude Code、Cursor、Codex などのAIエージェントが、依頼内容に応じて必要な情報だけを読めるドキュメント構造を検証することです。

## AIが最初に読む場所

AIエージェントはまず次を読んでください。

- [ai/index.md](ai/index.md)

READMEは人間向けの入口です。AIが作業判断をするための詳細は `ai/` 配下に集約しています。

## 構成

```text
project/
  README.md
  ai/
    index.md
    navigator.md
    operations.md
    state.md
    log.md
    architecture.md
    design.md
    coding_rules.md
    consideration.md
    features/
      todo.md
      auth.md
      notification.md
    skills/
      frontend.md
      backend.md
      graphql.md
      testing.md
```

## このサンプルの前提

- 題材は小規模なTodoアプリです。
- フロントエンドは React + TypeScript を想定します。
- バックエンドは Node.js + GraphQL を想定します。
- DBは PostgreSQL を想定します。
- 実装コードはありません。各Markdownは、実装がある場合にAIがどこを確認するべきかを示すサンプルです。

## 目的

一般的なREADME中心の構成では、AIが毎回README、設計資料、コード全体を広く読むことになりがちです。

このサンプルでは、次の状態を目指します。

- 依頼内容から読む資料を絞れる
- 作業中の状態を短く把握できる
- 有用な調査結果を次回以降に再利用できる
- 機能別の注意点に直接到達できる
- フロントエンド、バックエンド、テストなど作業種別ごとの知識を再利用できる
- 不要なコンテキスト投入を避け、Token消費を抑える

## 運用の考え方

このサンプルの `ai/` は、AIエージェントが参照するSchema兼Wikiです。

- `index.md`: 最初に読む入口
- `navigator.md`: 依頼内容から読む資料を選ぶルーター
- `operations.md`: Ingest / Query / Lint 相当の運用ルール
- `state.md`: 現在の作業状態
- `log.md`: AIによる更新履歴
- `features/`: 機能ごとの仕様
- `skills/`: 作業種別ごとの知識

AIは毎回ゼロから情報を探し直すのではなく、作業で得た再利用可能な知見を必要に応じて `ai/` 配下へ反映します。
