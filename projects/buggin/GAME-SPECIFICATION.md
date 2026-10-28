# Buggin? — Game Specification

**Working title:** Buggin? (subject to name/availability checks)  
**Tagline direction:** “Tiny Bugs. Big Problems.”  
**Platform:** Roblox, mobile and desktop

## Vision and core loop
A colorful, mischievous asymmetric multiplayer game: one human survives on a tabletop while multiple tiny mosquitoes navigate obstacles and launch themselves from slingshots. This is a free-movement physics playground, not a tower-defense game. Mosquitoes walk and jump during normal movement; they do not fly except during slingshot attacks. Use the standard Roblox mobile joystick and desktop controls.

## Rounds and maps
- One human versus the remaining players as mosquitoes. Choose the human randomly, reducing selection weight for recently selected humans.
- Round duration configurable, initially around 3–5 minutes; intermission around 30 seconds.
- Human wins by surviving until time expires. No overtime solely because a mosquito has not landed a final shot.
- Mosquitoes respawn after about 5 seconds indefinitely. Late joiners join as mosquitoes. If the human leaves, mosquitoes receive partial contribution rewards. A player who leaves and rejoins must not double-claim a round reward.
- First map is a living-room tabletop with household props such as Rubik's cubes, cups, stationery and blocks. Provide multiple natural routes and obstacles, not fixed lanes or a rigid grid.
- Map vote shows three random choices after the first 10 seconds of intermission. Difficulty multipliers start at Normal 1.0×, Medium 1.25×, Hard 1.5×. Hard maps may include narrow paths and water hazards.
- Human teleports to a fixed map spawn and places defenses during the live round, not during a separate setup phase.

## Haven, movement and slingshot
- Mosquito Haven is the respawn area and includes a pool/water feature. Mosquitoes emerge from a bottle cap sequence before teleporting to the active map.
- Reaching a slingshot automatically launches the mosquito stinger-first at the human. The human cannot interrupt an already launched mosquito; valid hits deal damage and the mosquito respawns.
- Damage per launch scales inversely with the number of mosquitoes, with configurable bounds so small and large servers remain viable.
- Validate launch, cooldown, hit, damage and rewards on the server. Prevent forged hits and repeated triggers.
- Human health bar and username remain visible. Results show role, Sugar Tokens, EXP and level progress.
- A valid lethal shot at the final second may trigger a special all-player animation and goofy human death effect; provisional rare badge: “The Last-Minute Shot”. Server validates the result before awarding it. Prevent duplicate outcomes/rewards.

## Story and presentation
A skippable opening cutscene: two mosquito buddies discover a sugar cube in a glue trap; one gets stuck and signals the other to run. The main mosquito escapes but loses its wings, reaches a high place, sees a human on a table and frowns. Skipping uses a majority vote. Human wins can trigger map-specific animations, e.g. flinging a bottle cap away.

## Human defenses
- Five loadout slots. Slot 1 is free; slots 2–4 unlock through levels (about every five levels, configurable) or Robux; slot 5 is a paid unlock.
- Configure loadout during intermission. In-round placement has a valid green preview, drag positioning, rotation, place and cancel by tapping the selected slot again.
- Touch controls must not conflict with camera movement. Placement is free on suitable surfaces, not grid-only.
- Server validates surface, map bounds, overlap, spacing, defense caps and placement rules. Prevent stacking exploits and prevent the human from blocking every essential route.

## Currencies, rewards and progression
Three distinct currencies:
- **Sugar Tokens:** earned standard currency; not tradable.
- **Sugar Crystals:** premium currency; tradable and usable for eligible purchases.
- **Sugar Cubes:** temporary mosquito upgrade currency; distinct from the other two.

Both teams earn Tokens and EXP based on contribution; human generally earns more to encourage the role. Use configurable, exploit-resistant formulas. Persistent EXP, level and Tokens survive rounds. Daily rewards grant **Sugar Tokens and cosmetics only**—no EXP and no Sugar Crystals—with server-enforced reset/streak and duplicate-claim protection.

Mosquito Elder sells temporary genetic upgrades such as speed, jump and health using Sugar Cubes. Limit levels; upgrades persist across respawns within a round and reset after the round.

## Inventory, skins and crates
- Inventory tabs: Defences and Mosquito Skins. Include rarity colors, sorting, previews, ownership and equipped state. Locked items cannot be equipped; server validates ownership.
- Skins are cosmetic only; animations/effects are okay but no gameplay stats.
- Defenses and skins come from crates, not a direct item shop. Sugar Tokens buy ordinary crates; Sugar Crystals buy premium crates. Limited-time crates may later contain time-limited content.
- Crates are a later rollout: architect extension points now but do not let them block the core loop. Prices, odds, availability, pity threshold and duplicate policy must be configurable; display odds transparently.

## Lobby and UI
- Attractive, colorful lobby with clear, compact navigation: Inventory, Crates, Loadout, Rewards. Show level and Sugar Tokens clearly. Avoid pointless decorative NPCs and unnecessary Settings buttons.
- Loading screen has mosquito-themed animation/VFX, game title, genuine progress feedback and rotating tips. Load player data and essential assets before enabling gameplay; handle errors safely.
- UI is release-blocking quality: coherent palette, typography, spacing, hierarchy, icons, states, animations and responsive mobile/desktop layouts. Use several references as inspiration, synthesize a cohesive design, inspect actual Studio screenshots and iterate. Check contrast, clipping, touch targets, safe areas, camera obstruction and scaling. Code running is not proof of UI quality.

## Monetization
Initial configurable Sugar Crystal pack ideas:
- 50 crystals / 50 Robux
- 100 / 100 Robux
- 300 / 250 Robux
- 600 / 500 Robux
- 1,300 / 1,000 Robux

Keep monetization configurable and avoid pay-to-win combat advantages. Crystals may be used for eligible crates/gamepasses and can be traded. Tokens cannot be traded. Defenses and skins are tradable by default, subject to provenance/admin restrictions. Use MarketplaceService receipt handling with durable idempotency, safe retries/recovery and server validation. Never invent production product IDs.

## Trading
- Defenses and skins tradable by default; Sugar Tokens never tradable; Sugar Crystals tradable.
- Some admin-granted/exclusive items have additional restrictions and may require owner approval.
- Each unique item gets a stable UID (example `ITM-7F3A91C2`); each trade gets a unique Trade UID. Track origin, ownership and trade chain.
- Crystal slider and numeric input stay synchronized; max respects balance and limits.
- Any offer change restarts a 5-second cooldown for both players. Both accept, then enter a 10-second confirmation phase. Both must explicitly confirm; countdown never auto-commits.
- Offer edits, cancellation, invalidation or disconnect abort confirmation and release reservations safely.
- Validate ownership, balance, eligibility, UIDs and trade state immediately before commit. Use reservations, transaction journals, idempotent operation IDs and recovery/compensation. Roblox DataStores do not provide general atomic cross-player transactions; do not promise this.
- Read-only trade history includes completed/cancelled/failed trades, time, players, items, crystals, reasons and UID links.

## Provenance and item flow
- Owner-only Item Flow Tree traces an item from origin (match reward, crate, purchase, admin grant, event) through trades to current owner across servers/time. Clickable player/trade/match/timestamp nodes, date filters and paginated expansion.
- Global historical search by username/UserId, including items no longer owned. Basic items still have UID/current owner/basic history; rare/premium/admin-exclusive items can have enhanced tracking.
- Flag duplicate UIDs and inconsistent ownership; quarantine item and block trades while investigated. Support durable revoke/destroy actions that survive reconnects, preserve recovery/audit trails, and do not auto-ban innocent players.
- Avoid global scans. Use indexed UID/UserId/trade/time records, pagination, async fetching, bounded caches, rate limits and DataStore budget awareness. DataStores are not arbitrary-query databases; document indexing/retention limits.

## Admin and owner
- `totemoflol` is immutable highest authority in the game system and cannot be demoted, removed or banned by the game's admin tools.
- Central role/permission matrix. Admins cannot manage/promote/demote/remove other admins; owner can. Moderators may handle player moderation/announcements but not item grants or whitelist changes unless explicitly permitted.
- Polished admin UI: start/end rounds, switch roles, teleport, spawn test items, inspect player/match data, grant items, create admin-only items, schedule timed events (e.g. 2× Tokens), announcements, provenance inspection, quarantine/revoke/destroy.
- Owner Requests tab approves/rejects special admin-item transfers. Pending item is locked; approval authorizes only that transaction and expires if the item/offer/trade changes.
- Durable grant/audit logs record actor, target, item/action, scope, timestamp, reason and result. Admins cannot edit/delete logs.
- Announcements like `totemoflol: hi`, with avatar and role badge. Server-local by default; global scope requires explicit confirmation. Events expire automatically; global events use supported Roblox messaging services.
- Kick, temporary/permanent global bans and unban. Persistent UserId enforcement across servers. Banned Players tab searches username/UserId and shows reason, moderator, issue time, duration/expiry, scope and history. Log unbans.

## Reports, moderation and replay
- Report categories: exploit, scam, swearing, harassment, other. Rate-limit reports; reports alone never automatically ban. No report-review notification is required to the reporter.
- Begin with a server-recorded event timeline for movement snapshots, slingshots, damage, placements, trades and suspicious actions. Add 3D replay only if the recorded data supports it; pause, rewind, camera angles, follow player and jump to report timestamp. Mark missing evidence/gaps honestly; this is not literal video.
- Chat evidence must respect supported Roblox APIs and privacy/moderation rules. Never claim access to all chat. Log admin review decisions.
- Suspicious activity feed supports filters, dates, pagination and clickable records. Alerts include duplicate UID, inconsistent ownership, rapid trading, repeated failed trades, moderation/admin activity. Alerts are investigation signals, not proof or automatic bans.

## Data security and architecture
- Use Roblox DataStoreService for persistence. Server-authoritative currency, ownership, rewards, placement, damage, launches, purchases, upgrades, trades, bans and permissions.
- Validate every remote and rate-limit sensitive actions. Prevent spoofing, fake contribution, duplicate rewards, item duplication, purchase bypass and receipt replay.
- Safe save/load includes retries, appropriate session handling, schema versioning/migrations, duplicate claim protection and recovery. Never overwrite real data with defaults after load failure; surface the failure and block unsafe saves/gameplay as needed.
- Avoid monolithic player keys; partition histories, paginate, monitor request budgets and handle partial failure. MemoryStore is for suitable ephemeral coordination, not permanent truth.
- Modular systems: rounds, data, movement/launch, defenses, upgrades, inventory, crates, rewards, trading, provenance, admin, moderation/replay, UI and shared config.
- Test core loop and then all remaining systems, multiplayer, mobile/desktop, edge cases, security, persistence, trade concurrency, purchases and regressions. Document what was actually verified in Studio and what remains unverified.
