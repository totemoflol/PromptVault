# Buggin? — Claude Code Mega-Prompt

Read `../../CLAUDE.md`, `GAME-SPECIFICATION.md`, and `DEVELOPMENT-PLAN.md` before acting. The specification is the durable source of truth; this file defines execution expectations. Do not depend on prior chat history.

## Mission

Rebuild the Roblox game **Buggin?** from its current cooked state into a polished, fully functioning game that follows `GAME-SPECIFICATION.md`. Do not stop at a demo or vertical slice. Complete and verify the full applicable scope: core gameplay, UI, progression, data integrity, trading, provenance, admin/moderation, and release testing. Crates may be staged for later rollout as specified, but architecture must support them.

Work autonomously with sound technical judgment. Do not ask approval for every small choice. Document important decisions and ask only when ambiguity creates material risk, data loss, cost, or a major product-direction choice. Be truthful about limitations and verification.

## Non-negotiable rules

1. **Inspect first.** Inspect the live Roblox Studio environment and available MCP tools, current hierarchy, relevant Obsidian vault notes, and existing Claude Code notification setup.
2. **Back up before destruction.** This project requires a clean slate. Back up the current place/project, verify the backup exists and is reasonably recoverable, then clear old maps, models, scripts, UI and other project objects, leaving minimum Roblox essentials. Never reuse old code, assets, UI, maps or architecture. Do not wipe before backup verification.
3. **Protect Obsidian.** Read relevant notes, preserve useful knowledge, and make targeted edits/additions only. Never replace the whole vault or overwrite unrelated notes. Keep project decisions synchronized.
4. **Protect secrets.** Inspect/reuse the existing notification integration without printing webhook URLs or credentials. Never commit API keys, tokens, webhook URLs, passwords or private data to this public repository.
5. **Use the real environment.** Use Studio/MCP for implementation, inspection, play tests and screenshots when available. Do not pretend unavailable tools work. If blocked, find a safe workaround and report limitations.
6. **Test, don't assume.** A generated script or successful tool call is not proof of functionality. Test real flows, failure paths, abuse cases and regressions.
7. **UI is release-blocking.** Create a design system, inspect real screenshots and iterate. Never call the UI done without visual review.
8. **Server authority.** Currency, ownership, rewards, placement, damage, purchases, trades, bans and permissions are server-validated.
9. **Safe persistence.** Never overwrite real player data with blank defaults after load failure. Preserve data and use safe retries/recovery.
10. **Continue through scope.** Follow `DEVELOPMENT-PLAN.md`; do not stop after the first playable round. If blocked, document the exact blocker, finish independent work and revisit it.
11. **Truthful status.** Separate implemented from tested in Studio. Never invent test results, screenshots, tool access, progress or notification delivery.
12. **Respect platform limits.** Roblox DataStores are not arbitrary-query databases and do not provide general atomic multi-player transactions. Chat evidence, replays and cross-server systems must use supported APIs.

## First actions — in order

### A. Reconnaissance
- Identify the active Studio place/project and inspect the current hierarchy and state.
- Inspect available Studio MCP actions for scripts, instances, properties, play sessions, output/errors, screenshots and testing.
- Inspect relevant Obsidian notes. Old project content is not to be reused, but knowledge may be useful.
- Inspect the existing Discord notification integration safely; reuse it if functional without revealing its secret URL.
- Record tools, constraints and findings in project notes.

### B. Backup and reset
- Create a backup of the current Roblox place/project using the safest available method.
- Verify it exists, is non-empty/valid and reasonably recoverable. If possible, inspect or open a copy rather than altering the original.
- Only after verification, clear the current Studio place of old project maps, models, scripts, UI and other objects, retaining minimum Roblox essentials.
- Confirm the hierarchy is clean and the backup remains available. Do not salvage old content.

### C. Plan and proceed
- Create a concise plan with milestones, dependencies, risks and test gates in the Obsidian vault and/or project docs.
- Do not pause for approval after planning. Proceed autonomously unless blocked by a material issue.
- Map every specification requirement to implementation and tests. Keep the checklist current.

## Product execution

Implement the requirements in `GAME-SPECIFICATION.md`. Prioritize a stable, polished core loop, then systematically complete the rest of the spec:

- **Core loop:** one human versus mosquitoes; fair human selection weighting; configurable rounds/intermissions; map voting; joins/leaves; timeout/death outcomes; respawns; final-second lethal shot; rewards without duplicates.
- **Map and movement:** obstacle-rich tabletop with multiple routes; mosquitoes walk/jump but do not fly during ordinary movement; Haven and bottle-cap entry; automatic slingshot with server-validated hit/damage and scaling based on server population.
- **Defenses:** five loadout slots, real-time free placement, preview/drag/rotate/cancel, touch-safe controls, server validation, collision/bounds/caps and prevention of stacking or complete route blockage.
- **Progression:** contribution-based rewards, permanent EXP/levels and Sugar Tokens, daily rewards with Tokens/cosmetics only, temporary Sugar Cube upgrades that reset at round end.
- **Monetization:** configurable Sugar Crystal packs; correct MarketplaceService receipt handling, idempotency, durable grant records and recovery. Never invent live product IDs or trust client purchase claims.
- **Data:** versioned schemas, safe load/save, appropriate session handling, migrations, retry/recovery, throttling handling and duplicate-claim prevention. Never save blank defaults over a failed load.
- **Trading:** unique item/trade IDs, 5-second cooldown after offer changes, both accept, then 10-second confirmation where both must explicitly confirm. Never auto-commit on countdown. Use reservations, journals, idempotency and recovery/compensation; be honest about non-atomic DataStore operations.
- **Provenance:** indexed/paginated UID and player history, owner-only item flow, historical search, duplicate UID alerts, quarantine, durable revoke/destroy and audit trail. Avoid unbounded global scans.
- **Admin/moderation:** immutable highest authority for `totemoflol`; central permission matrix; grants and owner requests; scoped announcements/events; kicks, global bans/unbans; durable logs; rate-limited reports and human review; no automatic bans solely from reports.
- **Replay:** record a useful server event timeline. Build 3D replay only where captured data supports it; clearly show evidence gaps and do not present it as literal video. Respect Roblox chat/privacy/moderation APIs.
- **Crates:** architecture/config for later rollout; configurable prices, odds, availability, pity and duplicate policy. Do not let crates block the core game.

## UI and visual identity — highest priority

The experience must feel like a polished, cohesive Roblox game, not generic placeholder UI.

- Use a colorful, playful and slightly mischievous visual direction appropriate to tiny mosquitoes versus a human. Develop consistent palette, typography, spacing, hierarchy, icons, rarity colors, states and animation rules.
- If web/reference access is available, inspect several relevant references and synthesize their useful patterns into a cohesive design. Do not copy one screen blindly and do not stall if reference access is unavailable.
- Plan screens and reusable components before building the full UI. Document a short design guide.
- Build a polished mosquito-themed loading screen with title, animation/VFX, real progress feedback, rotating tips and safe data/loading error states.
- Build compact lobby navigation for Inventory, Crates, Loadout and Rewards; clearly show level and Sugar Tokens. Avoid pointless decorative NPCs and unnecessary Settings buttons.
- Build readable HUD, human health/username, mosquito UI, placement controls, upgrade UI, vote UI, cutscene skip, results, inventory, trading, admin, logs and flow-tree interfaces as required.
- Inspect real Studio screenshots. Iterate on hierarchy, alignment, contrast, spacing, clipping, scaling, touch targets, safe areas, camera obstruction, mobile portrait and desktop layouts.
- Do not declare UI verified if screenshot inspection or device testing was unavailable; state the limitation clearly.

## Testing workflow

Use `DEVELOPMENT-PLAN.md` as the live checklist. After each milestone:
1. Inspect Studio hierarchy, output/errors and current state.
2. Run relevant play tests with multiple players where possible.
3. Test failure and abuse cases, not only the happy path.
4. Capture and inspect screenshots for UI milestones.
5. Fix regressions before dependent work proceeds.
6. Update docs with verified status and remaining issues.

At minimum test round transitions, vote ties, joins/leaves/reconnects, respawns, human departure/death, final-second shot, mobile/desktop controls, placement edge cases, route blocking, reward duplication, daily claims, save/load failure, throttling, migrations, purchase receipt retries, concurrent/partial trades, provenance search/quarantine/revoke, admin boundaries, spoofed remotes, bans/unbans, report rate limits, evidence gaps, mobile UI, performance and remote spam.

## Communication

Use the existing Discord webhook notification setup if it is present and safe. For long sessions, send a meaningful progress update every 10–15 minutes and at major milestones: completed work, what was verified, blockers and next steps. Avoid spam. Never print webhook secrets or claim delivery without confirmation.

## Completion standard

Continue until all feasible requirements have been implemented and tested or a specific tool/platform blocker is documented. Final reporting must separate **Implemented**, **Tested in Roblox Studio**, **Partially verified**, **Blocked / not started**, and **Known platform limitations**. Link statuses to actual evidence. Never describe untested features as finished.
