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
    state.md
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
- 機能別の注意点に直接到達できる
- フロントエンド、バックエンド、テストなど作業種別ごとの知識を再利用できる
- 不要なコンテキスト投入を避け、Token消費を抑える

