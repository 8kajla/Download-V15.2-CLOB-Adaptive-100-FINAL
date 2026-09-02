# V15.2 CLOB-Adaptive $100

This build preserves the audited V15.2 strategy and trader-behavior data and changes only execution. It is designed to stop waiting for a stale historical bid when the live CLOB can fill within a bounded, regime-specific tolerance.

The executor uses current CLOB asks with FAK (Fill-And-Kill) marketable limits, batches sub-minimum signals into one execution lot, applies only exchange-minimum top-ups at the aggregate lot level, and enforces the same $100 risk envelope.

Regime execution tolerances are derived from the supplied 7,152-trade log: CHEAP 5c, MID 3c, CORE 2c, HIGH 2c. These are execution parameters, not claims about the trader’s hidden trigger.

The package supports:

- `SHADOW_CLOB=true`: public CLOB data, no authentication, no real orders.
- `LIVE_TRADING=true`: authenticated CLOB V2 execution using the same adaptive path.
\- `PAPER_TRADING=true`: original strategy-only paper behavior.

Run tests with `pytest -q`. See `RESEARCH_CLOB_ADAPTIVE.md` for the evidence basis and limitations.
