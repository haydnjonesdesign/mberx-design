# Tipping — Design Brief

> **For:** designer · **Status:** draft · **Date:** 17 Nov 2026
> **Evidence:** `ux-audit/espn-footytips/espn-footytips-aleague-tipping-ux-spec.md` (reference product) + `AGENTS.md`
> **Model:** the tipping card belongs to the sports code, not to a comp. One set of picks per round, used by every competition the player is in for that code.

## 1. Snapshot

MberX has two sports codes, AFL and NRL. A player tips a round once, per code. Those picks are the master card: every competition the player is in for that code reads from it — the default MberX Competition they are put in at signup, and any public or private comps they have joined since. So this screen is not comp-scoped. There is no comp picker, and there is no second round of tips to enter.

## 2. The moment

It is Thursday night. The player is on the couch, phone in one hand, half-watching the pre-game. They have two minutes and no patience. Their job is: see this week's games, pick winners, get out. Switching to the other code should feel like turning a page, not starting again.

The second, less happy moment is Sunday morning, when they remember they forgot and one game has already started. Same screen, and it has to be honest in both.

## 3. Goals

- A player can submit a full round of tips in under 60 seconds from opening the app.
- A player can always tell what is open, what has locked and what they have picked — and if they missed one, understand it in a glance.
- A player never submits a partial round without knowing it is partial.
- A player tips once and never repeats the round for another comp.
- A player can see how everyone tipped once the round has locked.

## 4. Scope

**In**

- AFL and NRL, switched on the screen.
- One round per code, with two-way picks.
- Per-fixture lockout at scheduled kickoff.
- Submission, confirmation, locked, live and results states.
- Byes, postponed and void fixtures.
- Code-wide sentiment once the round has locked.

**Out**

- Choosing, creating or joining comps. Comps consume the card; they are not managed here.
- Comp ladders and standings (linked to, not designed here).
- Per-comp tips. There is no such thing.
- Mini games, currency and rewards.
- Other sports or leagues.
- Margin, streak or any second scoring mode. One scoring model only.
- Odds, prices, or anything that reads as a market.
- Notification settings beyond a single reminder entry point.

## 5. Required functions

| # | What the player must be able to do | Why it matters |
|---|---|---|
| F1 | Know which code and which round they are tipping | Two codes run at once, with different rounds |
| F2 | Switch code without losing picks already made in the other | Half a round in each code is normal on a Thursday |
| F3 | Pick a winner for each open fixture, one of two teams | This is the entire task |
| F4 | Change a pick until that fixture locks | Regret is normal and cheap to allow |
| F5 | See at a glance which fixtures are open, locked, or already picked | State is the product, not a detail |
| F6 | See how much of the round is left to tip | "Have I done them all?" is the question |
| F7 | Understand that one set of tips covers every comp they are in | Otherwise they look for a comp picker that isn't there |
| F8 | Submit the round, and know it went through | Silent success reads as a failed tap |
| F9 | See their picks still in place after submitting | Proof that the app kept them |
| F10 | See each result as correct, incorrect or void, with a reason for void | A missing result is a support ticket |
| F11 | Understand a bye without thinking something is broken | Absence needs a label |
| F12 | Understand what happened when they missed a lockout | The most common unhappy path |
| F13 | See how everyone tipped, once the round has locked | The banter half of the loop |
| F14 | Get to their comps after submitting | Tipping is a means to the ladder |

## 6. States and edge cases

| State | When it happens | What the designer must show |
|---|---|---|
| Nothing tipped yet | Round open, no picks | The list is the empty state — no scolding, no modal |
| Partly tipped | Some picks made | Progress in plain words: "3 of 8 picked" |
| All picked, not submitted | Every open fixture has a pick | Submit becomes the obvious next action |
| Submitted | After submit | Inline confirmation with the round and time; picks stay visible |
| Fixture locked, not tipped | Kickoff passed with no pick | The fixture shows locked, and that no tip was recorded |
| Round fully locked | All fixtures started | The list becomes a record, not a form |
| Live | Games in progress | Which games are live, picks still visible |
| Partial results | Some fixtures resulted, some not | Per-fixture results, no round total until it is true |
| Void fixture | Postponed, abandoned, no result | "No result", the reason, and that nobody scores from it |
| Drawn match | A game finishes level, and no one could tip a draw | Still open — see section 10 |
| Bye | A team has no fixture this round | A compact row that says bye, not a missing card |
| No fixtures at all | Off-season, or a round not yet drawn | A designed empty state, not a blank screen |
| Submit failed | Network drops mid-submit | The picks are kept, and the retry is obvious |
| Duplicate submit | Player taps twice on a flaky connection | One round submitted, no double record |
| Default membership | Player is only in the MberX Competition | The card works exactly the same; no prompt to join a comp |
| Both codes partly tipped | Picks in AFL and picks in NRL | Each code keeps its own picks; switching back shows them |
| One code locked, one open | AFL live while NRL is still open | Each code shows its own state, with no cross-talk |

## 7. Recommended components

| Need | Recommended component or pattern | Reuse or new |
|---|---|---|
| Code and round context | Sticky header pairing the code with its round and lockout time | Reuse app header, add a round bar |
| Code switch | Two-option segmented control, AFL / NRL, sitting above the round | New |
| Scope line | One sentence, shown once under the round header | New |
| Fixture and pick | Fixture card with two large tap halves, sized for the longest abbreviated team name | New — the core component of this screen |
| Pick indicator | Filled half plus a check plus the team name, never colour alone | New |
| Locked fixture | Padlock plus the word "Locked" and the kickoff time | Reuse status chip |
| Round progress | Count in the header: "3 of 8 picked" | New |
| Submit | Sticky bottom action that states what it will submit | Reuse `Button / Primary` |
| Confirmation | Inline banner under the header, not a modal | New — no success pattern exists |
| Missed lockout | Inline notice on the fixture, with a way to the comps | Reuse `Inline notice` |
| Bye | Compact single-line row inside the date group | Reuse fixture row, collapsed |
| Result | Badge per fixture: correct, incorrect, void, with reason | Reuse status chip |
| Sentiment | Simple bar with percentages, showing percentage of tips for each team. | New |
| First-time explainer | One inline line above the list, expandable | New |

## 8. Screens and flow

```
Code (AFL) ⇄ Code (NRL)
Tipping (open) → Submit → Confirmation → (locked) → Results → Comps
```

| Screen | Purpose |
|---|---|
| Tipping — open | Pick and submit the round |
| Tipping — locked | Record of picks, with results as they land |
| Confirmation | Proof the round was submitted, with a way back |

One card per code, switched in place — switching does not navigate away from the round. Results are the same screen with results filled in, not a separate destination. If a state from section 6 needs its own surface, say so rather than stacking modals.

## 9. Content and tone

- **Voice:** matey and brief. Australian English. Funny about football, never about money or someone losing.
- **Words to avoid:** odds, bet, punt, price, wager, stake, "lock in your bets", "guaranteed".

| Where | Copy |
|---|---|
| Code switch | AFL · NRL |
| Scope line | One set of tips. Every comp you're in gets them. |
| Primary button | Submit tips |
| Progress | 3 of 8 picked |
| Confirmation | Tips are in for Round 14. |
| First-time explainer | One point per correct tip. Tips lock at kickoff. |
| Missed lockout | This one's locked. You didn't get a tip in. |
| Locked fixture | Locked · 7:40 pm |
| Void | No result. No points for anyone. |
| Bye | Bye this round |
| Empty round | No games this round. Check back Thursday. |
| Submit failed | Didn't go through. Your tips are still here — try again. |

## 10. Constraints, decisions and open questions

**Constraints**

- Mobile first, one hand. The whole round must be tippable with a thumb.
- Tips lock at each fixture's scheduled kickoff, not at round start.
- 44px minimum touch targets, 4.5:1 text contrast, state readable without colour.
- No odds, prices or market language anywhere on the screen.
- AFL and NRL only.
- Scoring is displayed, never recalculated in the client.
- No new nav item, no new tab.
- Times are shown in AEST/AEDT (Sydney time).
- Tips are per code, never per comp. The screen never asks which comp to tip for.
- Comp presence is one line of copy. No count, no list, no picker.

**Decisions**

| Question | Decision |
|---|---|
| Scoring model | Flat: one point per correct tip. |
| Are draws allowed? | No. Two-way picks only, in both sports. |
| What happens to a void fixture? | Void for everyone. Nobody scores from it. |
| Is sentiment visible before lockout? | No. Percentages appear only once the round has locked. |
| Round size and longest name | 8 fixtures per round. Longest team name is "Greater Western Sydney Giants" — design the card against it. |
| Who owns the reminder? | The app, not the comp captain. |
| Timezone on the lockout time | AEST/AEDT (Sydney time). |
| What is the unit of tipping? | The sports code. One master card serves every comp. |
| Which comp is the default? | The global MberX Competition, which every player is in automatically. |
| Does the screen carry a code switch? | Yes. Two options, AFL and NRL. |
| What happens on switching code? | It lands on that code's current round, not the same round number. Picks in both codes are kept. |
| How much comp information shows? | One sentence. Nothing else. |

**Still open**

| Question | Who decides | What it blocks |
|---|---|---|
| When a fixture finishes level and no one could tip a draw, how is it scored? | Product | The drawn-match state, and whether it reads as incorrect or void |

## Appendix — what the reference product got right and wrong

From the ESPN FootyTips audit. Copy the pattern, not the page.

**Worth keeping**

- Fixtures grouped by date with kickoff and venue in the card header.
- One large tap area per outcome, with the pick visible on the card afterwards.
- Per-fixture lockout, and the round staying on screen as a record after it locks.
- Community tip percentages — a genuinely good reason to come back after lockout.

**Worth avoiding**

- Decimal prices beside each outcome. In a free product they read as odds and invite a betting reading. Percentages only, after lock.
- A margin input that appears on one fixture with no label saying it is the margin game.
- Submit always enabled, including with zero tips picked.
- Notification consent bundled into the same card as tip submission.
- The ladder disappearing on mobile in the main mode.
- Five notification checkboxes on the tipping screen at all.
- A news carousel inside the task surface. Editorial belongs somewhere else.
- A comp-first header. The reference is code-first, and that is the right frame — comps consume the tips, they are not the unit of work.
