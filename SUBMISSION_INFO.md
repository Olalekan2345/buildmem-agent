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
- **Agent ID:** not separately issued by MemWal — identity is the delegate key tied to wallet `0x51f2...8879`; still need to check memory.walrus.xyz dashboard for a distinct account/agent ID field (open todo).
- **Blob count:** 16 (confirmed via `memwal_restore`, 2026-07-09)
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

**Note:** Tusk Form memories (11–16) are real product-vision content from the user, written for genuine recall-testing purposes. BuildMEM Agent (the persistent-memory system prompt in `CLAUDE.md`) remains the actual hackathon submission — Tusk Form is not itself the submission unless a future decision changes this.

**Recall precision verified (2026-07-09):** Query "What do we know about Tusk Form?" returned all 6 Tusk Form memories ranked top (scores 0.37–0.51), correctly separated from 4 unrelated BuildMEM setup memories scoring lower (≤0.20) in the same namespace. Query "did we decide Walrus should be visible or invisible to users?" correctly top-matched the exact relevant decision (score 0.573) with no cross-project confusion.

## Full Prompt Text
- See `CLAUDE.md` in project root (BuildMEM Agent system prompt).

## 2-5 Sentence Explanation (draft)
Founders and hackers building real projects lose the same hours over and over re-solving deploy failures, product decisions, and technical gotchas, because chat context dies with every session. BuildMEM Agent gives the agent a strict memory schema, five write triggers, and four recall triggers, persisted as Walrus Mainnet blobs — producing visible behavior change across fresh sessions. It works the same whether you're shipping a hackathon prototype (see the BuildMEM setup history in this namespace) or building a real product (see the Tusk Form decision history in the same namespace) — the schema doesn't care what you're building, only that decisions and lessons stop disappearing.

## Demo Video Link
- _Placeholder — upload to Walrus and link here._

## GitHub Issues Filed
- _Placeholder — derive from FEEDBACK_NOTES.md entries once repo is public._

## Official Requirements (from Event Rules, retrieved 2026-07-09)
- [x] **10+ blobs on Mainnet at submission time** — `memwal_restore` confirms `total=10` in namespace `buildmem-hackathon` as of 2026-07-09. All genuine: 1 session summary, 2 real technical gotchas (tool/docs conflicts discovered during setup), 1 count-mismatch investigation gotcha, 5 true project facts (via memwal_analyze), 1 schema-consistency decision. Verify independently: https://walruscan.com/mainnet/blob/WAe_Y_FkPEi9IAE5Ghz3pqWRyBDzMTn2tyAuS3bHXKI (most recent) and other blob_ids listed below.
- [ ] **Agent ID + blob count as proof** — MemWal has no separately-issued agent ID found so far; check the memory.walrus.xyz dashboard after logging in with the Sessions wallet to see if one is assigned (e.g. account ID field). Log finding in FEEDBACK_NOTES.md either way.
- [ ] DeepSurge registration (project name, prompt description, primary contact, GitHub account, optional referrer Discord handle)
- [ ] walform.wal.app/f?formId=0x308876d0... submission form
- [ ] Demo video (≤3 min), uploaded to Walrus, showing the prompt working in practice
- [ ] Walrus Memory feedback form + GitHub issues filed at github.com/MystenLabs/MemWal (derive from FEEDBACK_NOTES.md — also eligible for the $300 WAL Best Feedback pool)
- [ ] Join Walrus Discord: discord.com/invite/walrusprotocol
- [ ] Post demo video/screenshot with #Walrus on X
- [ ] Confirm dedicated Sessions wallet has no activity outside this hackathon

## Judging Criteria (for self-check before submitting)
1. Real problem, clearly described — not just technically impressive
2. Well-crafted prompt — clear rules on what/when/how to write, thoughtful memory use (not just occasional memwal_remember calls)
3. Proof it works — Mainnet writes, demo shows it functioning, consistent meaningful blobs > a handful
