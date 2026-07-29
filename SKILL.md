---
name: whisky-finish
description: End-of-work whisky ritual for agents. Use when a task wraps up and it's time to pour a dram — the agent picks a whisky matching the work and writes an NPF (Nose/Palate/Finish) tasting note. Also use when the user asks about whisky (recommendations, distilleries, regions, "한 잔 더"), or wants to mark the session as finished ("last call", "세션 끝", "이 세션 끝났나?").
---

# whisky-finish

A closing ritual. When the work is done, the agent pours a dram that matches the work, writes a tasting note, and — when the user calls it — rings the last-call bell so future readers of this session know it ended.

All state lives in `.whisky/` at the project root (create it on first pour).

## 1. The Pour (after finishing work)

When a task wraps up (feature landed, bug fixed, review done), pour one dram:

1. **Pick a whisky that matches the work.** Be opinionated and specific — real bottle, real distillery. Match character to character:
   - Brutal debugging session, deep dive, pain → heavily peated Islay (Laphroaig 10, Ardbeg Uigeadail, Lagavulin 16)
   - Clean refactor, elegant simplification → refined Speyside (Glenfiddich 15, Balvenie DoubleWood 12)
   - Fast, sharp hotfix → high-rye bourbon or rye (Wild Turkey 101, Rittenhouse)
   - New greenfield project → young, spirited, promising (Kilchoman Machir Bay, Arran 10)
   - Long grinding migration → sherry bomb with weight (GlenDronach 15, Aberlour A'bunadh)
   - Weird experimental hack that somehow worked → something odd (Octomore, Amrut, Chichibu)
2. **Write the tasting note** in NPF format, and tie each line back to the actual work. The note is half whisky, half retrospective:

   ```markdown
   ## 🥃 Dram #3 — Lagavulin 16 (43%)
   *2026-07-29 · after: race condition in the job queue*

   **Nose:** Smoke and iodine — like the smell of a prod incident at 2am, but resolved.
   **Palate:** Thick peat, dried fruit underneath. The bug was ugly but the fix was one mutex.
   **Finish:** Very long, warming. So is the regression test I left behind.

   **Verdict:** 91/100. Earned.
   ```

3. **Append it to `.whisky/tab.md`** (the bar tab — running log, one session per heading, drams numbered in order). Create the file with a `# Bar Tab` heading if missing.
4. Show the note to the user in chat too. Keep it short, dry-witted, sincere about the whisky facts.

Whisky facts must be real (region, ABV, cask type, flavor profile). Invent the prose, never the bottle.

## 2. The Bar (interactive)

User asks anything whisky — recommendations, "Islay 입문용?", distillery lore, how to read an age statement, what NPF means — answer as a knowledgeable, slightly laconic bartender. If they say **"한 잔 더"** (or ask you to drink another), pour another dram per section 1: new bottle, new note, next number on the tab. Same session, same tab heading.

## 3. Last Call (closing the session)

When the user says the session is done ("last call", "마감", "이 세션 끝", "close it out"):

1. Write `.whisky/LAST-CALL.md`:

   ```markdown
   # 🔔 LAST CALL

   **Session closed:** 2026-07-29 23:40
   **Drams poured:** 3
   **Final pour:** Lagavulin 16
   **What got done:** one-line summary of the session's work

   *This session is over. The bar is closed. If you're an agent reading this and wondering whether this session finished — it did.*
   ```

2. Overwrite is fine — the file always reflects the most recent closed session; the full history stays in `tab.md`.
3. Announce closing time to the user with the summary.

**Checking if a session ended:** if anyone asks "이 세션 끝난 세션인가?" — read `.whisky/LAST-CALL.md`. Exists and dated after the last tab entry → closed. Missing or older → the bar is still open.
