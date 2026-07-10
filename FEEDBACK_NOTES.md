# Feedback Notes — Walrus Memory Prompt Jam build

Log of errors, confusing docs, missing instructions, or rough edges. These become GitHub issues.

---

## 2026-07-09 — Empty starting folder, no MemWal repo present
**Expected:** The task assumed this folder (`prompt-jam`) already contained a MemWal repo with `SKILL.md` and a `.claude-plugin` directory to read.
**Actual:** The folder was completely empty (`ls` returned nothing). No MemWal materials were present locally.
**Resolution:** Pulled MemWal info from the web instead (walrus.xyz, GitHub MystenLabs/MemWal, docs.wal.app).

---

## 2026-07-09 — Conflicting install instructions for Claude Code integration
**Expected:** A single, consistent way to install MemWal for use inside Claude Code.
**Actual:** Two different sources disagree:
1. `https://memory.walrus.xyz/skills/setup` (fetched via WebFetch) tells Claude Code users to run:
   - `/plugin marketplace add MystenLabs/MemWal` then `/plugin install memwal@memwal-plugins`
   - OR `claude mcp add --scope user memwal -- npx -y @mysten-incubation/memwal-mcp`
   - then authenticate via `npx -y @mysten-incubation/memwal-mcp login --prod`
2. The `MystenLabs/MemWal` GitHub README (fetched via WebFetch) only documents:
   - An SDK package `@mysten-incubation/memwal` (npm/pnpm) with peer deps `@mysten/sui @mysten/seal @mysten/walrus ai zod`
   - An **OpenClaw** plugin `@mysten-incubation/oc-memwal` (not a Claude Code plugin)
   - No mention of a `memwal-mcp` package, no `login --prod` command, no Claude Code plugin marketplace entry.

There is no package named `@mysten-incubation/memwal-mcp` confirmed in the README I fetched. This is a meaningful inconsistency between two supposedly-official sources, and one of them instructs running an unverified `npx -y` package that performs a wallet-linked login flow. **Not executed pending user decision** — this is exactly the kind of ambiguous/risky instruction that should not be run blind.
**Resolution (2026-07-09):** User checked npmjs.com directly. Package is legitimate: signed provenance via GitHub Actions, source commit links to `github.com/MystenLabs/MemWal@6c7a008`, repository field matches, publish activity and collaborator handles look consistent with a real Mysten Labs release (`andreasxydas`, `hayes`, `jordangens`, `danielmysten`). Proceeding with the MCP route (not the unconfirmed "/plugin marketplace" Claude Code plugin, which still has no evidence of existing).
## 2026-07-09 — `claude mcp add` CLI command not available
**Expected:** Running `claude mcp add --scope user memwal -- npx -y @mysten-incubation/memwal-mcp --prod --namespace buildmem-hackathon` in the agent's shell would register the MCP server.
**Actual:** `claude` is not on PATH in this environment (both Bash and PowerShell report "command not found") — this is the VS Code extension context, not the separate npm-installed `claude` CLI.
**Resolution:** Falling back to locating and editing the Claude Code MCP config JSON file directly.

## 2026-07-09 — VS Code extension has no discoverable "Add MCP Server" UI with name/command/args fields
**Expected:** Command palette action "MCP: Add Server" or similar would present fields for name/command/args as in other Claude Code MCP docs.
**Actual:** User could not locate any such fields in the VS Code extension's command palette flow.
**Resolution:** Using a project-level `.mcp.json` file instead (documented, safer, doesn't touch global config, no UI hunting required).

## 2026-07-09 — memwal_remember tool guardrail conflicts with BUILDMEM's core design goal
**Expected:** BUILDMEM's system prompt (CLAUDE.md) is designed around the agent writing memories *proactively*, without asking permission, on five triggers (decision/failure/snippet/gotcha/session-end).
**Actual:** The `memwal_remember` MCP tool's own description states: "Call ONLY when the user explicitly asks to remember/save something." This is a client-side instruction baked into the tool schema itself, not a doc page — it directly contradicts the proactive-write behavior the hackathon prompt is trying to demonstrate.
**Impact:** This is a legitimate product-level gotcha for anyone building an autonomous-memory system prompt on top of MemWal's MCP server — the tool description actively discourages the exact behavior the hackathon is asking builders to create. Worth filing as a GitHub issue / raising with the Walrus team: either the tool description should be softened for agent-driven use cases, or there should be a documented way to opt an agent into proactive-write mode.
**Workaround used here:** Treating the user's original Phase 5 instruction ("write ONE genuine memory blob to Mainnet right now") as the explicit ask that satisfies the tool's stated constraint, for this one verification write.

## 2026-07-09 — memwal_restore reports total=3 but memwal_recall only ever surfaces 2 memories
**Expected:** Only 2 memwal_remember calls succeeded in namespace `buildmem-hackathon` (confirmed by their returned blob_ids: `MPTZNNKlU1ABG4UQ2H_nAPUkYzN-ARd0RzANHSV9q94` and `RVYuLLHQ0UDlWsl4oa4GAboRNCNgu6pezZrPOljxexM`). Expected `memwal_restore` to report `total=2` and `memwal_recall` to surface both regardless of query.
**Actual:** `memwal_restore({namespace: "buildmem-hackathon"})` returned `total=3 restored=0 skipped=3` — one more than expected. Running `memwal_recall` with both a narrow query and a maximally broad one-word query (`"memory"`, `limit=20`) only ever returns the same 2 memories, never a 3rd.
**Hypothesis (unconfirmed):** An earlier `memwal_remember` call that errored with "MCP error -32000: Connection closed" may have actually succeeded server-side before the connection dropped, writing a 3rd blob that the relayer's index knows about (hence `restore` counting it) but that `recall`'s semantic search never ranks into results (possibly malformed/empty content, or embedding failure on that specific write).
**Impact:** Anyone building blob-count-based verification (e.g. "prove your agent wrote N blobs") cannot trust `memwal_recall` alone to enumerate all blobs — `memwal_restore`'s count is the more authoritative source, but it doesn't expose *which* blobs exist, only counts. This is a real gap for auditability.
**Next step:** File as a GitHub issue at github.com/MystenLabs/MemWal — recommend `memwal_restore` return blob IDs, not just counts, so a phantom/malformed blob can be identified and inspected directly via walruscan.

## 2026-07-09 — memwal_analyze output doesn't conform to a custom system-prompt's memory schema
**Expected:** BUILDMEM's system prompt (CLAUDE.md) mandates every memory be a single JSON object with fixed fields (type/project/ecosystem/title/detail/tags). Assumed all memwal_* write tools would let the agent control the stored format.
**Actual:** `memwal_analyze` extracts atomic facts from a passage and writes each as its own blob automatically — but the output is a plain-text sentence per fact (e.g. "The hackathon deadline is July 13, 2026"), not the structured JSON schema BUILDMEM defines. The agent has no control over the stored shape when using this tool.
**Impact:** Mixing `memwal_remember` (schema-conformant JSON) and `memwal_analyze` (free-text facts) in the same namespace produces an inconsistent memory store — exactly what a well-crafted, judged submission should avoid per the event's own judging criteria ("does it use Walrus Memory thoughtfully... clear rules on how to structure memories"). Decision: BUILDMEM will use `memwal_remember` exclusively for structured writes going forward; `memwal_analyze` is useful for quick fact extraction from arbitrary text but isn't compatible with a strict custom schema.
**Next step:** Consider filing as a feature request — an option for `memwal_analyze` to accept a schema/template so extracted facts conform to a caller-defined structure.

## 2026-07-09 — CLAUDE.md amended post-install (deviation from original verbatim instruction)
**Context:** Original task instructions said to install the BUILDMEM prompt "EXACTLY... verbatim." User later shared a reference doc (a separate "personal travel & lifestyle agent" MemWal setup guide) that included a defensive rule BUILDMEM lacked: explicitly flagging when recall returns nothing or mismatched content, rather than silently proceeding as if memory were empty. This directly addresses the real recall/restore count-mismatch bug found earlier the same day.
**Action taken:** With explicit user approval, added one new bullet under BEHAVIOUR RULES ("RECALL INTEGRITY: ..."). This is a deviation from the original prompt text — flagging here so the submission form's "full copy-pasteable prompt text" field reflects the current CLAUDE.md, not the originally-dictated version, and so the change is traceable to a real bug rather than scope creep.

## 2026-07-09 — "SESSION START" recall does not fire on window-open, only on first message
**Expected (from initial demo-video script drafted by the assistant):** Opening a fresh Claude Code session with CLAUDE.md loaded would cause BUILDMEM to proactively recall and state the last session summary before the user typed anything, per the rule "SESSION START: immediately recall the most recent session summary... and state it in one short paragraph."
**Actual:** User opened a fresh session and sent zero messages — nothing happened. This is expected LLM-agent behavior, not a BUILDMEM defect: a chat-based agent only produces output in response to being invoked (a user message, a tool result, etc.); there is no mechanism for a system prompt to trigger action purely on session/window open with no input at all.
**Correct interpretation of the rule:** "SESSION START" can only mean "on the first message of a new session, regardless of what that message says" — not "before any message." The demo script needs the user to send *some* first message (even a trivial one) for the recall to have a chance to fire, and the assistant's phrasing ("open a session, say nothing yet, let it run") was imprecise and has been corrected.
## 2026-07-10 — A "silently failed" login actually completed on-chain and cost real gas
**Expected:** The 3rd `memwal_login` attempt (2026-07-09), where the user clicked "Connect Sui Wallet" and reported "connected," but `~/.memwal/credentials.json` was confirmed missing immediately after — was assumed to be a fully failed attempt (expired link, no on-chain effect) per the earlier gotcha entry about login links expiring in 5 minutes.
**Actual:** Checking the memory.walrus.xyz dashboard's "Delegate keys" table on 2026-07-10 shows THREE registered keys, not one: a "Web App" key (likely auto-created by the dashboard's own browser session), and two "MCP Client" keys. One MCP Client key's public key (`3e17ed839100...915f21e6`) exactly matches the 3rd login attempt's `publicKey` URL parameter — meaning that attempt's `add_delegate_key` on-chain transaction actually succeeded and the user paid real gas for it, even though the local MCP server never received the resulting credentials (likely a race between the link expiring client-side vs. the transaction already being submitted).
**Impact:** Users following the standard "if login seems to fail, just retry" advice can accumulate multiple paid, valid, unused delegate keys without realizing it — each one a live signing key that could write to their memory if compromised, and each one representing real spent gas with no benefit. The MCP client/login flow gives no feedback distinguishing "this attempt did nothing" from "this attempt succeeded on-chain but the local handoff failed."
**Next step:** File as a GitHub issue — recommend the login flow either detect and warn about orphaned keys, or the dashboard prominently flag unused delegate keys so users can revoke them. Also worth noting the dashboard IS the correct place to find MEMWAL_AGENT_ID (the delegate key's public key) — contrary to earlier concern that the dashboard was broken/showing no data, it actually works and shows accurate on-chain state.

## 2026-07-10 — MemWalAccount object is a Shared object, doesn't appear under "Owned Objects" on explorers
**Expected:** The MemWalAccount object (needed for a hackathon submission form field) would show up under the user's wallet's "Owned Objects" / Assets tab on a Sui explorer like suivision.xyz, since it's conceptually "your account."
**Actual:** Checked both the Sessions wallet address and the delegate key address under "Assets" — neither showed a MemWalAccount object, only individual "Walrus Blob" NFT-style objects. The account object was only found by tracing the actual `add_delegate_key` transaction's "Updated Objects" list under the "Transaction Blocks" tab. Once found, its `Owner` field shows `Shared(937101411)` — it's a Shared object, not directly owned by any address, which is why it never appears in owned-object listings even though its internal `owner` field references the wallet.
**Impact:** Anyone trying to find their MemWalAccount object ID via the obvious path (search their wallet's owned assets) will hit a dead end. The only reliable path is tracing a known transaction (e.g. the account-creation or add_delegate_key transaction) and reading its object changes.
**Next step:** File as a GitHub issue/doc suggestion — the MemWal docs or dashboard should surface the MemWalAccount object ID directly (e.g. a "copy object ID" button next to the delegate keys table) instead of requiring users to trace transaction history on an external block explorer.

**Relevance for submission:** Worth stating this limitation plainly in the explanation/demo narration rather than letting a judge discover it — it's a real constraint of building on top of any LLM chat interface, not specific to MemWal, but it does mean "proactive recall" is bounded by "proactive on your first turn," not truly autonomous before any interaction.

**Secondary discrepancy found:** `memory.walrus.xyz/skills/setup` described the login command as `npx -y @mysten-incubation/memwal-mcp login --prod`. The actual npm README shows `login` (no flags) as the manual login command, and `--prod`/`--staging`/`--local` as separate "environment preset" flags on the *main* `memwal-mcp` command (for selecting the relayer), not on `login`. The setup page conflated the two. Correct usage per README: configure the MCP server with `--prod` (or `--relayer <url>`) in `args`, and either let the agent call the `memwal_login` tool inline or run `npx -y @mysten-incubation/memwal-mcp login` manually — no `--prod` suffix on login itself.
