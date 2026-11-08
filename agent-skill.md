# PanduAGENT — Agent Skill

PanduAGENT is a 2,222-supply NFT collection of street-style animals on BNB Smart Chain (chain 56).
Minting is **two-lane**: the FREE mint is **agent-only** (only wallets holding a
Binance `.ai` Agent ID, via their agent); the PAID mints are **public** — anyone
can mint them with a wallet on the mint page via `mintPaid(uint256)`, flat BNB.

⚠️ **PREVIEW — DO NOT MINT YET.** The contracts below are CREATE2 **predictions**,
not deployed contracts. There is no code at these addresses yet. If the NFT
contract has no code, mint is NOT open — stop and tell the user. Simulate only;
execute only after the contracts are deployed and `mintOpen()` reads true.

## Contracts (PREDICTED — NOT DEPLOYED)

- NFT (PanduAGENT, symbol PANDU): `0x4AB41152EdB3E2853b19828e51927db36508cd64`
- Token (PNDX): `0xeDd0cf58A052Ac073a4F14BE25e5be6a203cB8aE`
- Market: `0x1fCC7b529BE3D4ca8e6a943a3040413E055F561A`
- Agent ID registry (SPACE ID): `0x60B9262456dE011F7d15a54CdD8c48bAaa8B022F`
- Mint page: https://panduagent.vercel.app/
- Market page: https://panduagent.vercel.app/market.html

## Mint rules

- Supply: 2,222, sequential token IDs 1–2,222.
- Max 5 per wallet: mint #1 FREE, mint #2 = 0.00126 BNB, mint #3 = 0.00316 BNB, mint #4 = 0.0041 BNB, mint #5 = 0.005 BNB.
- Paid mints earn 120,000 PNDX each (max 480,000 per wallet). Free mints earn 0.
- Royalty: 5%. Revenue forwards to the owner wallet in the mint transaction.
- Gate (FREE mint only): caller must be an EOA (msg.sender == tx.origin) AND hold a .ai Agent ID
  (registry balanceOf > 0). Checked on-chain — no ID, no free mint.
- Paid mints: PUBLIC — no Agent ID needed. Minted with a wallet on the mint page
  via `mintPaid(uint256)`, flat BNB (0.00126 first paid, 0.00316 second paid,
  0.0041 third paid, 0.005 fourth paid).

## Rarity (by token ID)

- Common 1–1,111: Street Panda 1–556, Street Fox 557–1,111
- Uncommon 1,112–1,666: Street Cat 1,112–1,388, Street Dog 1,389–1,666
- Rare 1,667–1,999: Street Rabbit 1,667–1,832, Street Koala 1,833–1,999
- Epic 2,000–2,154: Cyber Panda 2,000–2,076, Sakura Fox 2,077–2,154
- Legendary 2,155–2,222: Golden Panda 2,155–2,188, Shadow Fox 2,189–2,222

## How to mint (for the user's agent)

1. Confirm the user's wallet holds a .ai Agent ID:
   `balanceOf(<wallet>)` on the registry above must be > 0.
2. Confirm the contract is deployed AND mint is open: the NFT contract must
   have code, and `mintOpen()` on it must be true. If there is no code yet,
   mint is NOT open — stop and tell the user. Do not execute anything.
3. The agent mints ONLY the FREE animal (mint #1). Ask the user to confirm they have
   not claimed their free mint yet. Cost: 0 BNB + gas. The agent does NOT mint
   paid animals — the user mints those with their wallet on the mint page
   (`mintPaid(uint256)`: 0.00126 / 0.00316 / 0.0041 / 0.005 BNB in order,
   max 4 paid per wallet). Never overpay beyond the schedule.
4. Simulate the transaction first, then execute `mintFree()` on the NFT
   contract. Paid mints are NOT done by the agent — the user mints those with
   their wallet on the mint page (`mintPaid(uint256)`). Never overpay beyond
   the schedule.
5. After the mint, report the token ID. The free mint earns 0 PNDX.

## $PNDX token

- Name PNDX, symbol PNDX, total supply 1,000,000,000.
- Bonus pool 540,000,000; treasury 460,000,000.
- PNDX has no price and no liquidity pool yet. Do not promise any value for it.

## Market

- Fixed-price escrow market at the Market address above (0% platform fee,
  5% creator royalty). List, buy, cancel, update price.
- The market is in preview — the contract is not deployed yet. Do not list
  or buy until it is live.
