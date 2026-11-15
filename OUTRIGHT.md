# Outright program qualification

This is a development fork of [aeyakovenko/percolator-prog](https://github.com/aeyakovenko/percolator-prog), based on upstream commit `7b11091328de23cded2e4afe96592bbd060a6828`. The upstream history, license and attribution are retained. The Percolator engine dependency is `5e3af0710ec7e9b7077393012f8a94a31b2f07ef`; its source is used without local accounting changes.

## November 15 upstream integration

The candidate merges eleven upstream program commits and the matching nine-commit
engine update. Live value exits now check unsettled positions on their own asset,
and trade admission bounds the work needed to refresh liened claims. Single and
batch trade regressions cover that bound, including lapsed source domains.

The engine update corrects resolved-close ledger recovery, liquidation behind
lapsed backing, loss payments funded by liened claims, provider withdrawals before
winners settle, and repayment of provider principal after a late resolved loss.
Outright's Recovery observation correction and independent model/fixture repairs
below remain present. No account-layout or instruction-encoding change was found
in the reviewed diff; Rust conformance and full qualification must verify that
for the exact candidate before adoption.

## Changes under qualification

- Allow an asset already in Recovery to use its frozen, committed state during account-health progress. The oracle profile is still validated. Live and DrainOnly assets retain their existing freshness checks. Tests cover delayed Recovery, malformed and stale Live observations, omitted evidence, rollback, custody and the original maximum-shape compute limits.
- Align reward fixtures with the existing authenticated-price provenance rule. Trade-origin catch-up still cannot earn rewards merely because a fresh external target was published. Positive receipt tests first authenticate the effective price through a public crank; negative controls retain zero unauthorized rewards.
- Compare funded report histories using their exact input-derived funding. Different observation histories can legitimately accrue different funding; identical histories with different account-settlement timing must still reconcile exactly.
- Reconcile rounded per-leg exposure with aggregate open interest in the independent test model. Exact aggregate accounting, an independent ADL index/epoch history, canonical raw-basis transitions and scoped terminal-removal witnesses remain checked. The retained failure is replayed through both permissionless progress and owner exit. No arbitrary one-atom tolerance is added.

## Evidence and release status

The [Outright application repository](https://github.com/TheTradoor/outright) owns the pinned-source qualification workflow, native client integration and release checklist. Each result must identify the exact source and SBF artifact it executed. Passing a focused regression does not substitute for the complete wrapper gates or current-validator integration.

This fork is not a mainnet deployment. A public release still requires complete qualification, a verified deployed program and market, operator-controlled authorities, live oracle and keeper operations, real-wallet acceptance and independent security review. The website's mainnet transaction path remains disabled until those prerequisites are met.
