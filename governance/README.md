# governance/ — 統制規約の骨子（目次と担当割り）

> Day 0 時点では目次と担当割りのみ。中身は受注後に各章を正式化する。
> 設定の正本参照: 第 5 章の branch protection / rulesets 一覧は `hardening/desired.json` を正本とする。

| 章 | 内容（骨子） | 担当（案） |
|---|---|---|
| 1. 統制方針 | 統制要求 ↔ 本 repo 群の対応表（要求→実装機構→証跡の 3 列） | 統制チーム |
| 2. アクセス統制 | org/teams/CODEOWNERS 設計・認証経路（git/Secret 非搭載） | 統制 + インフラ |
| 3. 監査証跡 | デプロイ sync 履歴 + git 履歴 + 改ざん防止監査ログの三点対応 | インフラ |
| 4. サプライチェーン | SBOM(syft) + cosign + pin 規約 | インフラ |
| 5. 変更管理 | フリーズ・CCB・非 waivable ゲート（= hardening/desired.json を正本参照） | 統制チーム |
