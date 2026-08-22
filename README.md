# Prediction Market Systems

Trading and settlement infrastructure for prediction markets — Polymarket execution
research, a copy-trading engine, and an on-chain pari-mutuel protocol.

Prediction markets are where most of my recent execution work has landed. Two of these
projects also anchor my [low-latency execution portfolio](https://github.com/pranay123-stack/low-latency-execution-systems);
they appear in both because they genuinely belong to both.

---

## Featured Projects

### Polymarket CLOB Execution Research — Rust
Where does theoretical edge actually disappear?

- Deterministic replay over a committed 2.8 MB recorded Polymarket BTC Up/Down session
- Exact `i128` Shapley attribution of edge loss, reporting its own rounding residue
- Measured-vs-assumed table so every input is labelled
- **177/177 tests pass** — independently verified by execution

[View repository →](https://github.com/pranay123-stack/polymarket-live-clob-research)

### Polymarket Copy-Trading Engine — Rust
Event-driven copy trading, paper and live behind one adapter seam.

- 13-crate workspace, **341 tests pass** (independently verified), zero `unsafe`
- Recovered the deployed EIP-712 signing scheme from mainnet — domain version `"3"`,
  not the documented `"1"` — and proved it by recovering signers of settled orders
- Concluded from its own measurements that venue publish delay (~400 ms), not internal
  latency, is the binding constraint

[View repository →](https://github.com/pranay123-stack/polymarket-copy-trading-hft-rust)

### MatchCall — Solana / Anchor
A trustlessly-settled World Cup prediction market.

- 929-line Anchor program implementing pari-mutuel escrow
- Permissionless settlement through an on-chain TxLINE `validate_stat_v2` CPI
- Program ID confirmed `executable: true` on devnet
- `reindex-from-chain.ts` — the kind of tool you only write after actually running it

This is the only prediction-market **protocol** here; everything else trades against one.

[View repository →](https://github.com/pranay123-stack/matchcall)

---

## Supporting Work

### NBA Playoffs Prediction Edge — TypeScript
Injury-driven signal generation with cross-market momentum-lag detection, built for a
DoraHacks hackathon.

**Honest status:** this has never traded. It runs in dry-run mode by default, and its
executor simulates latency, slippage and transaction hashes — which the README and the
code both state plainly. 18 tests. Treat it as a signal-pipeline prototype, not a
proven strategy.

[View repository →](https://github.com/pranay123-stack/nba-prediction-edge)

---

## Reproducing the verified numbers

```bash
git clone https://github.com/pranay123-stack/polymarket-live-clob-research
cd polymarket-live-clob-research && cargo test        # expect 177 passing

git clone https://github.com/pranay123-stack/polymarket-copy-trading-hft-rust
cd polymarket-copy-trading-hft-rust && cargo test --workspace   # expect 341 passing
```

### Related
Sports traded on betting exchanges rather than event contracts lives in
**[Algorithmic Sports Betting](https://github.com/pranay123-stack/algorithmic-sports-betting)**.
`nba-prediction-edge` and `matchcall` appear in both.

**Tech across this portfolio:** Rust, Tokio, Solana, Anchor, TypeScript, EIP-712

---

## Not currently working

### Polymarket HFT Arbitrage — Rust
36.5k lines across three venue adapters. **It does not compile** — `cargo build` fails, so
its 166 tests have never run. Its CI referenced a GitHub Action that does not exist, which
is why nothing caught it; that reference is now fixed so CI reports the true state.
Published because the architecture is worth reading, clearly labelled because it does not work.

[View repository →](https://github.com/pranay123-stack/polymarket-hft-arbitrage)

---

## Design Specifications *(not implemented)*

These repositories contain **architecture documents only — no source code**. They are
published as planning artefacts and each carries a banner saying so. Any latency,
throughput or performance figure in them is an unmeasured design target, not a result.

| Specification | Scope |
|---|---|
| [prediction-market-projects](https://github.com/pranay123-stack/prediction-market-projects) | Outcome tokens, LMSR/CPMM pricing, oracle resolution, futarchy |
