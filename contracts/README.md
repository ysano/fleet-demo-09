# contracts/ — IF 契約の SSOT

このディレクトリは machine-readable な IF 契約（OpenAPI 3.x）の source of truth。多チーム並列実装の
関所は、ここの契約に対して CI が破壊的変更検出・lint を実行し、consumer repo が pin 突合することで
成立する。規約の詳細は `dev-contracts` plugin の `contract-governance` skill を参照。

## 配置

```
contracts/
  <name>/
    openapi.yaml     # 契約本体。info.version が契約自身の semver
  contracts-versions.json  # {契約名: info.version} 集約（consumer への公開物）
```

## semver 運用（要約）

- **MAJOR**: 後方互換を壊す（endpoint/field 削除・required 追加・型変更・enum 削除）→ consumer 再実装
- **MINOR**: 後方互換な追加（optional field・新 endpoint・enum 値追加）
- **PATCH**: 意味を変えない記述修正（description/example/typo）

`info.version` の bump 方向は実 diff の破壊性と一致すること。破壊 diff なのに MINOR/PATCH のままだと
`contract-breaking-change` workflow が fail する。

## CI ゲート（このリポジトリ = control）

- `.github/workflows/contract-breaking.yml` — oasdiff で base との破壊的 diff を検出（ERR で fail）
- `.github/workflows/contract-lint.yml` — Spectral で `.spectral.yaml` に照らし lint（error で fail）

## consumer への公開

lint / 破壊検出を通した後、各契約の `info.version` を集約した `contracts-versions.json` を公開する。
consumer repo はこれを取得し、自 repo の `.contracts-lock.yaml` と `contract-pin` workflow で突合する。
