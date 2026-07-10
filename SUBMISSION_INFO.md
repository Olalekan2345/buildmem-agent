# Submission Info — BuildMEM Agent (Walrus Memory Prompt Jam)

## Project
- **Name:** BuildMEM Agent
- **Hackathon:** Walrus Sessions 5 — Walrus Memory Prompt Jam (Jun 26 – Jul 13, 2026)

## Dedicated Sessions Wallet
- **Address:** `0x51f2d246f0f193aa45af81d6afe260e6c681e99b14fce98d211cac3ff5428879`
- **Network:** Mainnet — confirmed by user on sign-in page and via walruscan.com/mainnet blob explorer links
- **Purpose:** Dedicated to this hackathon only, per submission rules. Do not reuse for other projects.

## Namespace
- `buildmem-hackathon`

## Verification (Phase 5 round trip — completed 2026-07-09)
- **First write (gotcha memory):** `blob_id` = `MPTZNNKlU1ABG4UQ2H_nAPUkYzN-ARd0RzANHSV9q94`
- **Explorer:** https://walruscan.com/mainnet/blob/MPTZNNKlU1ABG4UQ2H_nAPUkYzN-ARd0RzANHSV9q94
- **Recall confirmed:** same-session `memwal_recall` returned the exact blob content (score 0.658), proving the write/read round trip works on mainnet.
- **Agent ID (MEMWAL_AGENT_ID):** `0b5c3d11251930b321bb34c49648bb2dde4bc99d4904e82144fe3f41e563e0bb` — confirmed via memory.walrus.xyz/dashboard "Delegate keys" section, "MCP Client" key created 7/9/2026, matches the publicKey used in the successful memwal_login attempt and the credentials currently active in ~/.memwal/credentials.json. This is the key behind all 16 blob writes. Note: a second orphaned "MCP Client" key (3e17ed839100...915f21e6) exists from a login attempt that succeeded on-chain but never synced credentials locally — see FEEDBACK_NOTES.md, recommend revoking it.
- **Blob count:** 16 (confirmed via `memwal_restore`, 2026-07-09)
- **MemWalAccount object:** `0xf66586845ee9f65cabdc5a16ef2d5e4189703925e0cb2b2eb179b7f43ac14cdc` (type `0xcee7...24c6::account::MemWalAccount`, a Shared object referencing wallet `0x51f2...8879` as owner field). Explorer: https://suivision.xyz/object/0xf66586845ee9f65cabdc5a16ef2d5e4189703925e0cb2b2eb179b7f43ac14cdc
- **All blob IDs (namespace `buildmem-hackathon`):**
  1. `MPTZNNKlU1ABG4UQ2H_nAPUkYzN-ARd0RzANHSV9q94` — gotcha: memwal_remember tool conflict
  2. `RVYuLLHQ0UDlWsl4oa4GAboRNCNgu6pezZrPOljxexM` — session summary 2026-07-09
  3. `WqC0EPUns1Q2ooR1neAWoIl2j5BZgzWVOhVcKSvhxAo` — gotcha: restore/recall count mismatch
  4. `gRG-_l8nUpdNt9VyzCXMBt5lVVwCb5k82vu_f19FtUw` — fact: relayer URL for production
  5. `XUH7S90ZLdSwingu3UmjMnfZeSAdar1jddxgmh8bDEc` — fact: dedicated Sessions wallet
  6. `IIwCyDizULDuW7YZ87euqzdNLUaA2ElhlBtqvlF4vy0` — fact: hackathon deadline
  7. `izvzb31iy2BN_Hr26G2p6mS9ZpnMz4_DJVaFwTUfo80` — fact: results announcement date
  8. `9uhc_kzgqUti7HmQ5EaJGFEEpskxDflIwg3ejJKdlZw` — fact: 10-blob minimum requirement
  9. `WAe_Y_FkPEi9IAE5Ghz3pqWRyBDzMTn2tyAuS3bHXKI` — decision: schema consistency (memwal_remember only)
  10. _(one phantom/unrecovered blob — see FEEDBACK_NOTES.md "restore total vs recall" entry)_
  11. `-YjE2sstJyZ6DCPE4FQuPeTrFrLBVSv7U_akxLp9-00` — Tusk Form decision: feedback intelligence platform, not memory demo
  12. `tBZobwHsx9cNu_il3b4ylJECFC1PI7QspvcNO7qD7Z4` — Tusk Form decision: naming/branding
  13. `YXNKvmKP7sLIWFh1aWHKwzd0jqkg5LG9RgV-ch_G41g` — Tusk Form decision: Walrus as invisible infrastructure
  14. `UBsvGaPRYOzogJRfDSEkWe7h0t1uYgi45nrZRzkjR4M` — Tusk Form decision: core workflow
  15. `nOVbSRchSFRRkPsnCJw-oKXjxaWWBtF1E9n2bVYoAdA` — Tusk Form decision: planned intelligence features
  16. `TB-IRFFVMjYyU9NwvXF8SXuBD5r876qNn8d2jzsaLbQ` — Tusk Form feedback: hackathon-projects-start-with-people lesson

**Note:** Tusk Form memories (11–16) are real product-vision content from the user, written for genuine recall-testing purposes. BUILDMEM (the dev-memory system prompt in `CLAUDE.md`) remains the actual hackathon submission — Tusk Form is not itself the submission unless a future decision changes this.

**Recall precision verified (2026-07-09):** Query "What do we know about Tusk Form?" returned all 6 Tusk Form memories ranked top (scores 0.37–0.51), correctly separated from 4 unrelated BUILDMEM memories scoring lower (≤0.20) in the same namespace. Query "did we decide Walrus should be visible or invisible to users?" correctly top-matched the exact relevant decision (score 0.573) with no cross-project confusion.

## Full Prompt Text
- See `CLAUDE.md` in project root (BuildMEM Agent system prompt).

## 2-5 Sentence Explanation (draft)
Founders and hackers building real projects lose the same hours over and over re-solving deploy failures, product decisions, and technical gotchas, because chat context dies with every session. BuildMEM Agent gives the agent a strict memory schema, five write triggers, and four recall triggers, persisted as Walrus Mainnet blobs — producing visible behavior change across fresh sessions. It works the same whether you're shipping a hackathon prototype (see the BuildMEM setup history in this namespace) or building a real product (see the Tusk Form decision history in the same namespace) — the schema doesn't care what you're building, only that decisions and lessons stop disappearing. The prompt itself is fully portable: it contains no hardcoded wallet, namespace, or project-specific data, so anyone can copy `CLAUDE.md` into their own project and get the same behavior with their own MemWal login.

## Demo Video Link
- _Placeholder — upload to Walrus and link here._

## GitHub Issues Filed
- _Placeholder — derive from FEEDBACK_NOTES.md entries once repo is public._

