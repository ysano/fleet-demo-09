# Quick Spec: orders-api MVP デリバリ（リハーサル）

- Status: Approved（Sprint F リハーサル用）
- 契約正本: `contracts/orders-api/openapi.yaml`（1.0.0 公開済み）

## Stories

### Story 1: orders-api 契約 1.1.0 の互換拡張を公開する

**Size**: S
**Intent**: OrderCreate に optional `note` を追加した 1.1.0 を関所経由で公開し、contracts-versions.json を更新する。

#### Context
契約 1.0.0 は公開済み。consumer（fleet-demo-10）は 1.0.0 を pin 中。

#### Task
openapi.yaml に optional note を追加し info.version を 1.1.0 へ。contracts-versions.json を 1.1.0 に更新。

#### Verification
contract-lint / contract-breaking とも green で merge されること。

#### Boundaries
破壊的変更は含めない（required 追加禁止）。

### Story 2: consumer の pin を 1.1.0 に追従する

**Size**: S
**Intent**: fleet-demo-10 の .contracts-lock.yaml と checked-in contracts-versions.json を 1.1.0 へ更新する。

Blocked by #3

#### Context
Story 1 の公開が前提。

#### Task
lock と versions.json を 1.1.0 に bump する PR を作り、contract-pin green を確認して merge。

#### Verification
contract-pin が exit 0。

### Story 3: 初回 portfolio roll-up を baseline 記録する

**Size**: S
**Intent**: fleet 横断の初回 roll-up を実行し ci/dag/ 隣接の計測 baseline を残す。

Blocked by #4

#### Context
Story 2 完了後のデリバリ状態を初回計測とする。

#### Task
portfolio_rollup.py --file --since --until --scale fleet を実行し結果を記録。

#### Verification
roll-up 出力の repo_count が対象数と一致。
