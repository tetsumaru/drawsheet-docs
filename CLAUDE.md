# CLAUDE.md

## プロジェクト概要

Drawsheet の公開ドキュメントリポジトリ。ソースリポジトリ (`tetsumaru/drawsheet`) の `docs/` ディレクトリから自動同期される。

## 目的

Drawsheet は private リポジトリのため、API 仕様や用語集を外部に公開する目的で分離されたリポジトリ。

## ドキュメント構成

- `docs/api/` — OpenAPI 3.1 仕様 (`openapi.yaml`) と API リファレンス UI (`index.html`)
- `docs/terms/badminton/` — バドミントン用語集 (game, open, order, pair, team_match)

## 注意事項

- このリポジトリの内容はソースリポジトリから同期されるため、直接編集しない。変更は `tetsumaru/drawsheet` の `docs/` に対して行う。
- API 仕様は Firebase Callable 形式、Bearer トークン認証。
