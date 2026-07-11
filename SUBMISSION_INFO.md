# Submission Info — BuildMEM Agent (Walrus Memory Prompt Jam)

## Project
- **Name:** BuildMEM Agent
- **Hackathon:** Walrus Sessions 5 — Walrus Memory Prompt Jam (Jun 26 – Jul 13, 2026)
- **Repo:** https://github.com/Olalekan2345/buildmem-agent
- **DeepSurge:** https://www.deepsurge.xyz/projects/cda00470-30ad-415c-8084-305a8ca2a3c8
- **Demo Video:** https://youtu.be/LEYOiD7WFJg?si=gKksEk0UI0B7T0MP

## Dedicated Sessions Wallet
- **Address:** `0x51f2d246f0f193aa45af81d6afe260e6c681e99b14fce98d211cac3ff5428879`
- **Network:** Mainnet
- **Namespace:** `buildmem-hackathon`

## On-Chain Verification
- **Blob count:** 22 (confirmed via `memwal_restore`, 2026-07-11 — grew from 16 via separate sessions not tracked in this file's history, including real Tusk Form decisions finalized independently)
- **MEMWAL_AGENT_ID:** `0b5c3d11251930b321bb34c49648bb2dde4bc99d4904e82144fe3f41e563e0bb`
- **MemWalAccount object:** `0xf66586845ee9f65cabdc5a16ef2d5e4189703925e0cb2b2eb179b7f43ac14cdc`
  Explorer: https://suivision.xyz/object/0xf66586845ee9f65cabdc5a16ef2d5e4189703925e0cb2b2eb179b7f43ac14cdc
- **Example blob:** https://walruscan.com/mainnet/blob/MPTZNNKlU1ABG4UQ2H_nAPUkYzN-ARd0RzANHSV9q94

## Full Prompt Text
See `CLAUDE.md` in project root.

## Explanation
Founders and hackers building real projects lose the same hours over and over re-solving deploy failures, product decisions, and technical gotchas, because chat context dies with every session. BuildMEM Agent gives the agent a strict memory schema, five write triggers, and four recall triggers, persisted as Walrus Mainnet blobs — producing visible behavior change across fresh sessions. The prompt is fully portable: it contains no hardcoded wallet, namespace, or project-specific data, so anyone can copy `CLAUDE.md` into their own project and get the same behavior with their own MemWal login.

## GitHub Issues Filed
- https://github.com/MystenLabs/MemWal/issues/379 — docs.wal.app returns 403 to automated/non-browser fetches
- https://github.com/MystenLabs/MemWal/issues/380 — Setup guide conflates the --prod flag with the login subcommand
- https://github.com/MystenLabs/MemWal/issues/381 — memwal_remember tool description conflicts with proactive-memory agent use cases
- https://github.com/MystenLabs/MemWal/issues/382 — memwal_restore total count exceeds what memwal_recall can enumerate
- https://github.com/MystenLabs/MemWal/issues/383 — MemWalAccount object (Shared) is undiscoverable via normal wallet explorer views
- https://github.com/MystenLabs/MemWal/issues/384 — Login attempts that appear to fail client-side can silently succeed on-chain
