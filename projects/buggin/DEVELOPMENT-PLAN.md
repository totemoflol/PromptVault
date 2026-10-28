# Buggin? — Development and Verification Plan

Use this as a live checklist, not as permission to stop after the first playable prototype. Continue through all applicable phases, report blockers honestly, and track evidence.

## Phase 0 — Reconnaissance and safe reset
- [ ] Inspect Roblox Studio state, place/project identifiers, hierarchy, available MCP tools, runtime testing, output/errors and screenshots.
- [ ] Inspect relevant Obsidian vault notes. Preserve useful notes and make targeted edits/additions only.
- [ ] Inspect existing Claude Code notification setup without printing webhook secrets.
- [ ] Back up the current Roblox place/project and verify the backup exists and is reasonably recoverable.
- [ ] Only after backup verification, clear old project assets, code, UI, maps, models and objects, leaving minimum Roblox essentials. Do not reuse old architecture/assets.
- [ ] Record findings and create a concise plan, then proceed without waiting for approval except for material blockers or risky irreversible choices.

## Phase 1 — Playable foundation
- [ ] Define module boundaries, shared config, remotes, server authority and data schema.
- [ ] Build clean lobby and first tabletop map with multiple viable routes.
- [ ] Implement round/intermission state machine, human selection weighting, map vote, joins/leaves and win conditions.
- [ ] Implement mosquito walk/jump, Haven respawn, slingshot launch, server-validated damage, human health and results.
- [ ] Implement real-time defense placement and responsive placement UX.
- [ ] Test multiplayer state transitions in Studio before expanding.

## Phase 2 — Progression and presentation
- [ ] Implement contribution rewards, persistent EXP/levels, Sugar Tokens, daily rewards and temporary Sugar Cube upgrades.
- [ ] Implement loadout and inventory foundations; keep crate interfaces configurable for later rollout.
- [ ] Implement lore cutscene/skip vote, win animations and final-second lethal-shot handling.
- [ ] Build a coherent UI design system, loading screen, lobby, HUD, placement, results and responsive layouts.
- [ ] Inspect real Studio screenshots at mobile and desktop sizes; iterate until quality gates pass.

## Phase 3 — Persistence and monetization
- [ ] Add versioned schemas, safe load/save, session handling, retries, migrations and recovery.
- [ ] Simulate load/save failure, throttling, duplicate claims, disconnects and stale sessions.
- [ ] Implement configurable products and idempotent MarketplaceService receipt handling. Never invent production IDs.
- [ ] Verify failed or repeated receipts cannot grant duplicate currency/items.

## Phase 4 — Trading and provenance
- [ ] Add unique item/trade IDs, ownership/source records and trade history.
- [ ] Implement offer cooldown, accept/confirm phases, explicit confirmations, reservations, disconnect cancellation and transaction journal.
- [ ] Test concurrent trades, stale offers, edits, invalid ownership, insufficient balance and partial-failure recovery.
- [ ] Build indexed/paginated owner-only provenance lookup and flow UI.
- [ ] Test duplicate UID quarantine, revoke persistence and historical search.

## Phase 5 — Admin, moderation and audit
- [ ] Implement permission matrix and immutable owner authority for `totemoflol`.
- [ ] Build admin tools, grant/request flows, scoped announcements/events, bans/unbans and persistent logs.
- [ ] Implement rate-limited reports, human review, suspicious activity alerts and event timeline capture.
- [ ] Build replay UI only where data supports accurate reconstruction; mark gaps.
- [ ] Verify every privileged action server-side and log outcomes.

## Phase 6 — Content and release readiness
- [ ] Add/configure more maps and difficulty variants.
- [ ] Roll out crates only after core stability; configure odds/prices/availability/pity/duplicate policy and show odds transparently.
- [ ] Tune movement, damage, respawn, defenses and rewards across server sizes.
- [ ] Check mobile/desktop UX, readability, performance, network behavior and exploit resistance.
- [ ] Complete test matrix, fix regressions and update specification with verified status.

## Minimum test matrix
| Area | Required checks |
|---|---|
| Rounds | Intermission, vote ties, transitions, timeout, human death/leaves, final-second lethal shot |
| Players | Minimum player count, late join, disconnect/rejoin, respawn, transition leave |
| Movement | Mobile joystick, desktop controls, jumping, collision, hazards, slingshot cooldown/hit |
| Placement | Valid/invalid surface, overlap, boundaries, spam, stacking, touch/camera conflicts, route blocking |
| Rewards | Contribution formulas, partial round, duplicate claim, abandon/rejoin, daily claim, upgrade reset |
| Data | First join, returning player, load/save failure, throttling, migration, reconnect, concurrent session |
| Purchases | Valid/repeated/delayed receipt, failed grant recovery, forged client claims |
| Trading | Cooldown, accept/confirm, edits, disconnect, concurrency, insufficient balance, partial commit |
| Provenance | Origin, trade chain, UID/UserId search, pagination, duplicate UID quarantine, revoke persistence |
| Admin | Owner authority, forbidden admin actions, spoofed remotes, grant approval, event scope, ban/unban, logs |
| Moderation | Rate limits, false reports, evidence gaps, review audit, no automatic bans from reports alone |
| UI | Mobile portrait, desktop scaling, safe areas, readability, feedback, loading errors, camera obstruction |
| Performance | Larger servers, many defenses, history pagination, request budgets, update rates, remote spam |

## Release gates
A feature is complete only when requirements map to implementation, normal and failure/abuse paths are tested, integration/regression checks pass, and UI is visually reviewed where relevant. Use status labels **Implemented**, **Tested in Studio**, **Partially verified**, **Blocked**, or **Not started**. Code written is not proof of testing.
