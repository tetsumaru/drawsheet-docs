# API Gateway 経由での API 呼び出し

## 概要

Drawsheet の Cloud Functions API は API Gateway 経由で呼び出します。
クライアントは **Bearer トークン1つ** のみで認証できます。

## 呼び出し方法

```bash
curl -s -X POST \
  "https://${GATEWAY_HOST}/<endpoint>" \
  -H "Authorization: Bearer ${TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{"data": { ... }}'
```

- `GATEWAY_HOST`: API Gateway のホスト名
  - dev: `drawsheet-gateway-b3ttwoz8.an.gateway.dev`
  - prd: `drawsheet-gateway-4cwapjzw.an.gateway.dev`
- `TOKEN`: Drawsheet の API トークン（`/issue-token` スキルで発行）
- `<endpoint>`: `importTournament`, `createTournament`, `addParticipants`, `updateOrganization` など

## エンドポイント一覧

| エンドポイント | スコープ | 説明 |
|---|---|---|
| `/addParticipants` | `addParticipants` | 参加者追加 |
| `/createLeague` | `createLeague` | リーグ作成 |
| `/createOrganization` | `createOrganization` | 協会新規作成 |
| `/createTournament` | `createTournament` | 大会作成 |
| `/importTeamTournament` | `importTeamTournament` | 団体戦一括インポート |
| `/importTournament` | `importTournament` | 大会・参加者一括インポート |
| `/syncOrganizationMembers` | `syncOrganizationMembers` | 協会メンバー同期 |
| `/updateOrganization` | `updateOrganization` | 協会情報更新 |

## 旧 Cloud Run URL からの移行

以前の直接呼び出し（`https://asia-northeast1-PROJECT_ID.cloudfunctions.net/...`）は非推奨です。
外部クライアントからの直接呼び出しは拒否されます。

### 移行手順

1. API Gateway のホスト名を GCP コンソールで確認する
2. リクエスト先 URL を `https://GATEWAY_HOST/<endpoint>` に変更する
3. `X-Serverless-Authorization` ヘッダーが含まれていれば削除する（不要）
4. `Authorization: Bearer <TOKEN>` ヘッダーのみで呼び出す
