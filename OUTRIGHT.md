# Outright program qualification

This is a development fork of [aeyakovenko/percolator-prog](https://github.com/aeyakovenko/percolator-prog), based on upstream commit `357157e6e14d1d10ce78a995d5d50bb3c1f2ae13`. The upstream history, license and attribution are retained. The Percolator engine dependency remains `a712af767eeb217876a3d3c50e3849b60ea54462`; the engine's accounting implementation is not modified by this repair series.

## Changes under qualification

- Allow an asset already in Recovery to use its frozen, committed state during account-health progress. The oracle profile is still validated. Live and DrainOnly assets retain their existing freshness checks. Tests cover delayed Recovery, malformed and stale Live observations, omitted evidence, rollback, custody and the original maximum-shape compute limits.
- Align reward fixtures with the existing authenticated-price provenance rule. Trade-origin catch-up still cannot earn rewards merely because a fresh external target was published. Positive receipt tests first authenticate the effective price through a public crank; negative controls retain zero unauthorized rewards.
- Compare funded report histories using their exact input-derived funding. Different observation histories can legitimately accrue different funding; identical histories with different account-settlement timing must still reconcile exactly.
- Reconcile rounded per-leg exposure with aggregate open interest in the independent test model. Exact aggregate accounting, an independent ADL index/epoch history, canonical raw-basis transitions and scoped terminal-removal witnesses remain checked. The retained failure is replayed through both permissionless progress and owner exit. No arbitrary one-atom tolerance is added.

## Evidence and release status

The [Outright application repository](https://github.com/TheTradoor/outright) owns the pinned-source qualification workflow, native client integration and release checklist. Each result must identify the exact source and SBF artifact it executed. Passing a focused regression does not substitute for the complete wrapper gates or current-validator integration.

This fork is not a mainnet deployment. A public release still requires complete qualification, a verified deployed program and market, operator-controlled authorities, live oracle and keeper operations, real-wallet acceptance and independent security review. The website's mainnet transaction path remains disabled until those prerequisites are met.
