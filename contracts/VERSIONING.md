# 契約バージョニング規約

- 各契約は `contracts/<name>/openapi.yaml` の `info.version` を semver で管理する。
- **MAJOR**: 破壊的変更（endpoint 削除・request 必須追加・型変更等）。contract-breaking gate が FAIL で止める。意図的な破壊は MAJOR bump + maintainer の override 承認の 2 点セット。
- **MINOR**: 後方互換の追加（optional field・新 endpoint）。
- **PATCH**: 意味を変えない修正（description 等）。
- consumer への公開版は `contracts-versions.json`（`{契約名: info.version}`）を正とする。
- oasdiff semantics: response-only schema の required 追加は非破壊（破壊判定は request 文脈のみ）。
