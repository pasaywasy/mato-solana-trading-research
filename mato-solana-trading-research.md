# How do people actually trade on Solana in 2026?

**Research note** for Superteam Germany bounty slug `mato-research-how-do-you-actually-trade-on-solana`  
**Date:** 27 August 2026 (Europe/Berlin)  
**Method:** Public product docs, live venue UIs, and dashboard snapshots. **No survey. No invented percentages of “how traders feel.”** Volume figures below are dated snapshots, not a census of user behaviour.  
**Not financial advice.** Nothing here is a claim that any venue, order type, or duration produces profit.

---

## Why this note exists

Mato (München / Munich, founded 2025) is a Solana DEX whose pitch is a **Time-Weighted Order Book (TWOB)**: the trader sets size *and duration*; the book streams the order as a continuous flow and clears at a time-weighted price, with the stated goal of cutting sandwich surface and large-clip impact ([TWOB essay](https://thgehr.substack.com/p/twob); live UI: [mato.finance](https://www.mato.finance/)).

The Superteam Germany listing is not asking for a Mato brochure. It is paying six active traders for a **concrete walkthrough of a real recent trade**, a ≥$20 order on Mato, and a 45-minute call ([listing](https://earn.superteam.fun/listing/mato-research-how-do-you-actually-trade-on-solana/)). This note is complementary: a **map of the 2026 venue stack** so that those interviews can be read against what is actually live, and so that “how people trade” is not reduced to a single app screenshot.

---

## Snapshot of on-chain flow (known, dated)

[DefiLlama / Solana](https://defillama.com/chain/solana) on 27 August 2026 showed roughly:

| Metric | Snapshot |
| --- | --- |
| DeFi TVL | ~$5.89b |
| DEX volume (24h / 7d) | ~$2.37b / ~$20.6b |
| Perps volume (24h / 7d) | ~$1.49b / ~$12.6b |
| Active addresses (24h) | ~2.68m |
| NFT volume (24h) | ~$133k |

[DefiLlama Solana DEX rankings](https://defillama.com/dexs/chains/solana) the same day ranked **Pump** first on 24h venue volume (~$765m), then **Orca** (~$363m), **BisonFi**, **Meteora**, **Raydium**. Jupiter’s *own* listed DEX volume (~$87m) is **not** “Jupiter is small.” Jupiter Ultra is a **router**; most of what a user signs at [jup.ag](https://jup.ag/) lands in other venues’ pools. Treat aggregator UI share and venue volume as two different objects. **Unknown:** the share of that Pump/Orca/Raydium print that was clicked in Jupiter vs Phantom vs a memecoin terminal vs a Telegram bot.

Pump’s 24h **fees** on the same DefiLlama chain table (~$6.9m) were larger than Jupiter’s, Kamino’s, or Raydium’s. That is consistent with a market where **new-token flow, not SOL/USDC, is where a lot of the fee is**. It is not evidence that “everyone is a memecoin trader.”

---

## The stack people actually open

Retail Solana trading in 2026 is not one DEX. It is a **wallet → router → venue → (sometimes) another chain’s perps engine** pipeline.

### 1. Wallet as the front door: Phantom (and swaps inside it)

[Phantom](https://phantom.com/) is the default consumer wallet for Solana. People do not only “connect Phantom to a dapp.” Many swaps never leave the wallet UI. That is a product fact, not a survey: Phantom ships in-wallet swap, staking, and, since 8 July 2025, **Phantom Perps**.

**Phantom Perps is real.** Official product page: [phantom.com/perpetual-futures](https://phantom.com/perpetual-futures). Official learn article: [How to short crypto](https://phantom.com/learn/crypto-101/how-to-short-crypto). Specs the company publishes:

- In-wallet longs/shorts, mobile and web (Phantom Terminal on desktop).
- Up to **40×** leverage, **200+** markets (crypto, memes, and equity perps).
- **Powered by Hyperliquid**, not by a Solana CLOB. Funding is from the Solana wallet (any SOL token → position); settlement and matching live on Hyperliquid. Phantom’s own CLI/MCP docs describe the path: bridge into Hyperliquid spot, transfer to the perps account, then trade ([Phantom perps CLI](https://docs.phantom.com/phantom-cli/commands)).
- **Not available in all jurisdictions.** The product page says so in plain language. Availability for a given EU user is an empirical check inside the app, not a legal opinion in this note.

[The Defiant](https://thedefiant.io/news/defi/phantom-hires-ventuals-founders-after-hyperliquid-perps-venue-winds-down) reported Phantom’s own claim of **>$10b cumulative perps volume** within months of the July 2025 launch, plus a ~15–20m MAU / ~39% Solana wallet-share figure. Those are **company-reported**, not independently audited here.

**Known:** a large share of Solana users can open a leveraged book without leaving the wallet, and that book is Hyperliquid.  
**Unknown:** what fraction of “Solana traders” never touch a Solana perps venue at all because Phantom already routed them off-chain.

### 2. Default spot router: Jupiter Ultra, limits, DCA

[jup.ag](https://jup.ag/) is the default **spot** surface: Ultra swap, Limit, Recurring (DCA), Perps, prediction markets, tokenized stocks. Official Ultra docs ([Ultra Mode](https://docs.jup.ag/user-docs/trade/spot/ultra-mode)):

- Meta-aggregation across Solana AMMs plus RFQ/third-party sources (Metis, JupiterZ, DFlow, Hashflow, OKX, and others).
- Private landing (“Beam”), RTSE auto-slippage, optional gasless for small-SOL wallets.
- Published Ultra fees range **0–0.5%** by pair type (0% on some LST/stable routes; 0.5% on tokens <24h old). That is a **fee schedule**, not a promise of best execution.

Limit Order V2 ([docs](https://docs.jup.ag/user-docs/trade/swap/limit-orders)) is **not a CLOB**. Tokens sit in a vault; a keeper fires through Ultra when a USD-price or market-cap trigger hits. Output is **not guaranteed**. Stop-loss is explicitly **not guaranteed to fill** on thin names. Recurring/DCA V2 ([docs](https://docs.jup.ag/user-docs/trade/swap/recurring-orders)) splits a budget across time or a price band — the closest mass-market analogue to “trade over a duration,” and the thing Mato is trying to replace with a continuous clearing price rather than a sequence of discrete swaps.

**How people use it in practice (inferred from product design, not a poll):** one-shot Ultra for majors and “I just want out”; Limit V2 for “buy below / sell above” on names they already hold; Recurring for SOL accumulation. **Unknown:** fill rates on long-tail limits, and how often users abandon a limit because the vault hid the tokens from an airdrop snapshot (Jupiter documents that risk).

### 3. Liquidity venues the router hits

These are where size actually prints, even if the user never opens the site:

- **Pump / PumpSwap** — [pump.fun](https://pump.fun/). Bonding-curve launches; graduated flow into AMM liquidity. Largest 24h DEX print in the DefiLlama snapshot above.
- **Raydium** — [raydium.io](https://raydium.io/). Still a core AMM/CLMM the aggregator cannot skip.
- **Orca** — [orca.so](https://www.orca.so/). Whirlpools / concentrated liquidity; second on the 24h DEX table in this snapshot.
- **Meteora** — [meteora.ag](https://www.meteora.ag/). DLMM / dynamic pools; high fee capture relative to TVL in the same snapshot.

A user who “just swapped in Phantom” or “just used Jupiter” often paid **Pump or Orca or Raydium** on the other side of the route.

### 4. Memecoin terminals (the other “how”)

For new-token flow, the wallet swap box is often too slow. Public 2026 write-ups (not primary telemetry) consistently name **Axiom** ([axiom.trade](https://axiom.trade)), **Photon**, and **BullX** as the web terminals, plus Telegram bots (Trojan, etc.). Typical controls: preset buy size, slippage, Jito tip, snipe-on-create, wallet copy. Fees on these UIs are commonly advertised around **~0.75–1%** — an order of magnitude above Jupiter Ultra on majors.

**Known:** this class of product exists and is built around Pump.fun + Jito landing.  
**Unknown:** true market share. Third-party blogs quote Axiom “~50% bot share”; that number is **not** used here as a fact.

### 5. Solana-native perps: Jupiter Perps vs Drift/Velocity

**Jupiter Perps** is live on Solana ([docs](https://docs.jup.ag/user-docs/trade/perps)). Trader-to-LP against the **JLP** pool. Markets: SOL, ETH, wBTC. Max **250×**. Oracle-priced (Chaos Labs Edge primary; Chainlink and Pyth as checks). Two-step request + keeper fill. Limit orders are **not** liquidation protection; Jupiter says so. JLP holders are the counterparty: trader PnL is pool PnL.

**Drift** was the other headline Solana perps book. On **1 April 2026** it lost an estimated **$285m** after attackers obtained admin control (durable-nonce pre-signs + fake CVT collateral). Primary source: [Chainalysis](https://www.chainalysis.com/blog/lessons-from-the-drift-hack/). The project later rebranded toward **Velocity DEX**; [docs.drift.trade](https://docs.drift.trade/protocol) now describes Velocity Protocol as a reduced-surface fork focused on perps and lend/borrow (docs updated 27 August 2026). [The Defiant](https://thedefiant.io/news/defi/drift-protocol-rebrands-to-velocity-dex-ahead-of-relaunch) covered a July 2026 rebrand and a private beta, with public mainnet timing not nailed down in that report.

DefiLlama still listed a Drift row (~$294m TVL) on 27 August 2026. **Do not read that as “Drift is back at full public perps.”** TVL remnants, recovery vaults, and a live order book are different things. **Unknown:** where former Drift flow actually went (Jupiter Perps vs Phantom/Hyperliquid vs CEX vs sitting out).

### 6. NFTs: Tensor, not the same market

[tensor.trade](https://tensor.trade/) still presents as Solana’s professional NFT marketplace (order book + AMM-style inventory). DefiLlama’s **~$133k** 24h NFT print on the chain page is two orders of magnitude below DEX volume. NFT trading is a real venue and a small slice of “how people trade on Solana” in 2026.

---

## Execution reality: fees, MEV, duration

Solana has no public Ethereum-style mempool, but **ordering is still for sale**. Jito’s block engine runs a tip auction over bundles ([Jito docs](https://docs.jito.wtf/lowlatencytxnsend/)). Searchers can sandwich via `[frontrun, victim, backrun]` inside a bundle. Mitigations that actually exist:

- Tight slippage (Jupiter RTSE; terminals with manual caps).
- Private landing (Jupiter Beam / Ultra; wallet RPCs that forward to Jito).
- Jito **DontFront**: a read-only account whose pubkey starts with `jitodontfront` forces the protected tx to index 0 in any Jito bundle ([Solana docs](https://solana.com/docs/defi/mev-protection); [Jito sandwich mitigation](https://docs.jito.wtf/lowlatencytxnsend/#sandwich-mitigation)). Jito’s own disclaimer: **not a guarantee**, block-engine only, does not cover third-party ordering.

**Frankfurt is a Jito region, not a trading culture claim.** The block-engine table lists `https://frankfurt.mainnet.block-engine.jito.wtf` ([same Jito doc](https://docs.jito.wtf/lowlatencytxnsend/)). EU latency-sensitive flow *can* land through FRA. Whether Mato users, Phantom users, or Axiom users actually pin that region is **unknown**.

Jupiter Recurring and Mato TWOB are two answers to the same execution problem: **don’t dump size in one slot.** Jupiter does it as N discrete keeper swaps. Mato’s published mechanism does it as a continuous flow priced by USDC-flow / SOL-flow per slot ([TWOB](https://thgehr.substack.com/p/twob)). Mato’s live SOL/USDC ticket lets the user pick duration from 1 minute to 1 year ([mato.finance](https://www.mato.finance/)). **Unknown:** Mato depth, fill quality vs a Jupiter Recurring clip of the same notional, and whether anyone outside the research cohort uses it.

---

## How EUR actually becomes a Solana trade (EU facts only)

On-chain Solana does not take SEPA. The on-ramp is a **MiCA CASP** (or a leftover grey path that is now legally hostile).

- **1 July 2026** was the hard EEA MiCA enforcement date: no CASP licence, no EU clients. Kraken’s institutional note: [MiCA enforcement begins July 1](https://blog.kraken.com/product/kraken-institutional/mica-enforcement-begins-july-1). Kraken states MiCA authorisation via the **Central Bank of Ireland** and MiFID derivatives permissions via **CySEC**.
- **Backpack EU** (Solana-native CEX/wallet family) reported MiCA + payment-institution licences from Latvijas Banka (27 May 2026) on top of an existing CySEC MiFID entity — i.e. a regulated EUR → SOL/USDC door that is not “a DEX with a bank account” ([Solana Compass summary](https://solanacompass.com/news/backpack-eu-completes-eu-regulatory-trifecta-with-mica-and-payment-institution-licenses)).
- **Phantom Perps** and other derivatives UIs are **geo-restricted**. An EU user who can swap SOL in Phantom may still be blocked from the Hyperliquid perps pane. That is a product constraint, not a recommendation to VPN.

A factual EU path looks like: **EUR SEPA → licensed CEX (Kraken / Backpack EU / other CASP) → withdraw SOL or USDC to Phantom → spot on Jupiter/Phantom or perps if the app allows it.** Mato, Jupiter, and Drift/Velocity do not replace that first hop.

Mato’s own HQ being **München** is a team fact ([LinkedIn company page](https://www.linkedin.com/company/matofinance)), not evidence of a Frankfurt trading desk.

---

## A working picture of “how,” without fake surveys

Four loops show up in the **products people ship**, which is weaker than a diary but stronger than guesswork:

1. **Consumer spot.** Phantom or Jupiter Ultra. Size is “what’s in the wallet.” One signature. Router picks Pump/Orca/Raydium/Meteora. User never sees the pool.
2. **New-token / high-frequency.** Axiom / Photon / BullX / Telegram. Presets, Jito tips, failed txs as a cost of doing business. This is where most of the **fee** is in the DefiLlama snapshot, and where sandwich risk is highest.
3. **Leverage.** Either stay on Solana (Jupiter Perps vs JLP; historically Drift) or leave Solana without leaving the wallet (Phantom Perps → Hyperliquid). After April 2026, the second path is the one with a continuously documented consumer UI.
4. **Scheduled / duration.** Jupiter Recurring and Limit V2 are the mass options. Mato TWOB is the research-stage alternative: one order, one duration, continuous clear.

None of these loops has a public, high-quality **share of wallets** number. Anyone quoting “70% of German traders use X” without a method is inventing.

---

## Known vs unknown (explicit)

**Known**

- The live venues named above, with URLs, as of 27 August 2026.
- Phantom Perps exists and settles on Hyperliquid.
- Jupiter Ultra / Limit V2 / Recurring / Perps exist and are documented, including the ways they **fail** (stop-loss not guaranteed; output on Limit V2 not guaranteed).
- Pump leads dated DEX venue volume; NFT volume is tiny next to it.
- Drift’s April 2026 admin-key/durable-nonce drain is documented by Chainalysis; the successor surface is Velocity, not a quiet continuation of the old UI.
- Jito bundles, tips, DontFront, and a Frankfurt block-engine endpoint exist.
- EU CASP rules tightened on 1 July 2026; Kraken and Backpack EU publish MiCA-shaped on-ramps.
- Mato’s mechanism and UI exist; the Superteam bounty is a primary-research round, not a TVL contest.

**Unknown (and what would actually answer the bounty)**

- A real last trade: pair, size, venue, one-shot vs split vs limit vs DCA vs terminal, **all-in cost** (pool fee + Ultra/terminal fee + priority + Jito tip + failed-tx SOL), and what they would change.
- Slippage *realized* vs quoted, especially on Pump-age tokens.
- Whether EU users are systematically on CASP on-ramps or still using leftover accounts.
- Whether duration orders (Jupiter Recurring, Mato) are used for execution quality or just for not staring at the screen.
- Mato’s own book: opposite-side flow, unfilled inventory, and comparison vs an identical notional on Ultra.

That last block is exactly what the six paid walkthroughs are for. This note does not substitute for them.

---

## Sources

1. Superteam Earn listing — [https://earn.superteam.fun/listing/mato-research-how-do-you-actually-trade-on-solana/](https://earn.superteam.fun/listing/mato-research-how-do-you-actually-trade-on-solana/)
2. Mato live market — [https://www.mato.finance/](https://www.mato.finance/)
3. Gehrmann, *TWOB* — [https://thgehr.substack.com/p/twob](https://thgehr.substack.com/p/twob)
4. Mato (LinkedIn, München / 2025) — [https://www.linkedin.com/company/matofinance](https://www.linkedin.com/company/matofinance)
5. Jupiter — [https://jup.ag/](https://jup.ag/)
6. Jupiter Ultra Mode — [https://docs.jup.ag/user-docs/trade/spot/ultra-mode](https://docs.jup.ag/user-docs/trade/spot/ultra-mode)
7. Jupiter Limit Orders — [https://docs.jup.ag/user-docs/trade/swap/limit-orders](https://docs.jup.ag/user-docs/trade/swap/limit-orders)
8. Jupiter Recurring Orders — [https://docs.jup.ag/user-docs/trade/swap/recurring-orders](https://docs.jup.ag/user-docs/trade/swap/recurring-orders)
9. Jupiter Perps — [https://docs.jup.ag/user-docs/trade/perps](https://docs.jup.ag/user-docs/trade/perps)
10. Phantom Perps product — [https://phantom.com/perpetual-futures](https://phantom.com/perpetual-futures)
11. Phantom, *How to short crypto* — [https://phantom.com/learn/crypto-101/how-to-short-crypto](https://phantom.com/learn/crypto-101/how-to-short-crypto)
12. Phantom CLI perps — [https://docs.phantom.com/phantom-cli/commands](https://docs.phantom.com/phantom-cli/commands)
13. The Defiant on Phantom Perps / wallet share — [https://thedefiant.io/news/defi/phantom-hires-ventuals-founders-after-hyperliquid-perps-venue-winds-down](https://thedefiant.io/news/defi/phantom-hires-ventuals-founders-after-hyperliquid-perps-venue-winds-down)
14. Drift / Velocity docs — [https://docs.drift.trade/protocol](https://docs.drift.trade/protocol)
15. Chainalysis, Drift hack — [https://www.chainalysis.com/blog/lessons-from-the-drift-hack/](https://www.chainalysis.com/blog/lessons-from-the-drift-hack/)
16. The Defiant, Drift → Velocity — [https://thedefiant.io/news/defi/drift-protocol-rebrands-to-velocity-dex-ahead-of-relaunch](https://thedefiant.io/news/defi/drift-protocol-rebrands-to-velocity-dex-ahead-of-relaunch)
17. Pump.fun — [https://pump.fun/](https://pump.fun/)
18. Raydium — [https://raydium.io/](https://raydium.io/)
19. Orca — [https://www.orca.so/](https://www.orca.so/)
20. Meteora — [https://www.meteora.ag/](https://www.meteora.ag/)
21. Tensor — [https://tensor.trade/](https://tensor.trade/)
22. Axiom — [https://axiom.trade/](https://axiom.trade/)
23. DefiLlama Solana — [https://defillama.com/chain/solana](https://defillama.com/chain/solana)
24. DefiLlama Solana DEX volumes — [https://defillama.com/dexs/chains/solana](https://defillama.com/dexs/chains/solana)
25. Jito low-latency send / FRA engine / DontFront — [https://docs.jito.wtf/lowlatencytxnsend/](https://docs.jito.wtf/lowlatencytxnsend/)
26. Solana.com MEV protection — [https://solana.com/docs/defi/mev-protection](https://solana.com/docs/defi/mev-protection)
27. Kraken, MiCA 1 July 2026 — [https://blog.kraken.com/product/kraken-institutional/mica-enforcement-begins-july-1](https://blog.kraken.com/product/kraken-institutional/mica-enforcement-begins-july-1)
28. Backpack EU licences — [https://solanacompass.com/news/backpack-eu-completes-eu-regulatory-trifecta-with-mica-and-payment-institution-licenses](https://solanacompass.com/news/backpack-eu-completes-eu-regulatory-trifecta-with-mica-and-payment-institution-licenses)

---

*Written 27 August 2026. Figures from DefiLlama and third-party news are snapshots or reports, not a trader survey. Do not treat this as a reason to open a leveraged position or as a Mato performance claim.*

---

Licensed under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0).
