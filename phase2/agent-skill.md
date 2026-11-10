# PanduAGENT Phase 2 — Agent Skill

PanduAGENT Phase 2 is a 2,222-supply NFT collection of street-style animals on BNB Smart Chain (chain 56) — new outfits and new friends of Pandu. Minting is **two-lane + 5-pack**: the FREE mint is **agent-only** (only wallets holding a Binance `.ai` Agent ID, via their agent); the PAID mints are **public** — anyone can mint them with a wallet on the mint page via `mintPaid(uint256)`, flat BNB; and the **5-pack** mints all 5 animals in one transaction for a flat 0.0108 BNB.

✅ **LIVE — MINT OPEN.** Contracts deployed 10 Nov 2026, mint opened 05:23 UTC. NFT `0x9e5Dd59b5Df1d36de02454A1fD6d77ee5B07778B`, Market `0x92099c1142864b9d27258f2383C315789a66997C`, PNDX reused. Verify `mintOpen()` reads true before executing; if it reads false, stop and tell the user.

## Contracts (LIVE — deployed 10 Nov 2026)

- NFT (PanduAGENT Phase 2, symbol PANDU2): `0x9e5Dd59b5Df1d36de02454A1fD6d77ee5B07778B`
- Token (PNDX — REUSED from Phase 1, already deployed): `0xeDd0cf58A052Ac073a4F14BE25e5be6a203cB8aE`
- Market: `0x92099c1142864b9d27258f2383C315789a66997C`
- Agent ID registry (SPACE ID): `0x60B9262456dE011F7d15a54CdD8c48bAaa8B022F`
- Mint page: https://panduagent-phase2.vercel.app/
- Market page: https://panduagent-phase2.vercel.app/market.html

## Mint rules

- Supply: 2,222, sequential token IDs 1–2,222.
- Max 5 per wallet: mint #1 FREE, mint #2 = 0.00126 BNB, mint #3 = 0.00316 BNB, mint #4 = 0.0041 BNB, mint #5 = 0.005 BNB.
- 5-pack: `mintPack5()` — 5 animals in ONE transaction for a flat **0.0108 BNB** (20% off the 0.01352 BNB singles total, save 0.00272 BNB). Requires 0 mints so far; uses the full 5/wallet allowance. If the wallet holds an Agent ID, the first of the 5 is the free mint (4 paid); otherwise all 5 count as paid.
- Paid mints earn 120,000 PNDX each (max 480,000 per wallet — the PNDX token's wallet cap). A 5-pack accrues 480,000 PNDX either way (a public pack's 5th paid mint accrues 0). Free mints earn 0.
- Royalty: 5%. Revenue forwards to the owner wallet in the mint transaction.
- Gate (FREE mint only): caller must be an EOA (msg.sender == tx.origin) AND hold a .ai Agent ID (registry balanceOf > 0). Checked on-chain — no ID, no free mint.
- Paid mints: PUBLIC — no Agent ID needed. Minted with a wallet on the mint page via `mintPaid(uint256)`, flat BNB (0.00126 first paid, 0.00316 second paid, 0.0041 third paid, 0.005 fourth paid).

## Rarity (by token ID)

- Common 1–1,111: Hoodie Panda 1–556, Cap Fox 557–1,111
- Uncommon 1,112–1,666: Bomber Cat 1,112–1,388, Tracksuit Dog 1,389–1,666
- Rare 1,667–1,999: Raincoat Frog 1,667–1,832, Puffer Penguin 1,833–1,999
- Epic 2,000–2,154: Cyber Panda v2 2,000–2,076, Kimono Fox 2,077–2,154
- Legendary 2,155–2,222: Golden Panda 2,155–2,188, Shadow Fox 2,189–2,222

## How to mint (for the user's agent)

1. Confirm the user's wallet holds a .ai Agent ID: `balanceOf(<wallet>)` on the registry above must be > 0.
2. Confirm the contract is deployed AND mint is open: the NFT contract must have code, and `mintOpen()` on it must be true. If there is no code yet, mint is NOT open — stop and tell the user. Do not execute anything.
3. The agent mints ONLY the FREE animal (mint #1) — or the 5-pack if the user asks for it and has minted 0 so far. Ask the user to confirm they have not claimed their free mint yet. Free mint cost: 0 BNB + gas. The 5-pack costs 0.0108 BNB flat.
4. Simulate the transaction first, then execute `mintFree()` on the NFT contract — or `mintPack5()` for the pack (0.0108 BNB, wallet must have minted 0 so far). Singles (`mintPaid(uint256)`: 0.00126 / 0.00316 / 0.0041 / 0.005 BNB in order, max 4 paid per wallet) are minted by the user with their wallet on the mint page. Never overpay beyond the schedule.
5. After the mint, report the token ID(s). The free mint earns 0 PNDX; a pack accrues 480,000 PNDX.

## $PNDX token

- Name PNDX, symbol PNDX, total supply 1,000,000,000 — the SAME token as Phase 1 (already deployed, not redeployed for Phase 2).
- Bonus pool 540,000,000; treasury 460,000,000; max 480,000 per wallet.
- PNDX has no price and no liquidity pool yet. Do not promise any value for it.

## Market

- Fixed-price escrow market at the Market address above (0% platform fee, 5% creator royalty). List, buy, cancel, update price.
- The market is live — list, buy, cancel, update price.
- Element Market: the collection will also appear on Element Market (element.market) automatically after deploy — the exact collection link activates after indexing.

## Phase 1 (for reference only — sold out, do not mint there)

- Phase 1 NFT: `0x4AB41152EdB3E2853b19828e51927db36508cd64` — SOLD OUT 2,222/2,222. Never mint on it; Phase 2 is a separate contract.
