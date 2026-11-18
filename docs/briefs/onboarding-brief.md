# Onboarding — Design Brief

> **For:** AI design agent (Figma) · **Status:** draft · **Date:** 17 Nov 2026
> **Evidence:** `AGENTS.md` · `docs/briefs/tipping-brief.md` (the exit screen) · `docs/design/tipping-figma.md` (library keys and build lessons)
> **Target file:** https://www.figma.com/design/j3ET1PZaJSMKrJX2iFbgQb/Test (`j3ET1PZaJSMKrJX2iFbgQb`), design library attached as an asset
> **Model:** onboarding ends when the first tip is submitted. The player is auto-joined to the MberX Competition, so no comp step stands between them and a tip.

## 1. Snapshot

New players install MberX to tip footy with their mates. Onboarding must take a first-timer from a cold app to a submitted first tip as fast as honesty allows: welcome, confirm they are 18 or over, make an account with email, tell us what to call them, and land on the current round with a tip in. Everything that can wait, waits.

## 2. The moment

A mate mentioned MberX at the pub and they installed it on the couch, phone in one hand. They want to see this week's games and pick winners before the first bounce. They are curious, slightly impatient, and one confusing screen away from closing the app. The moment is not "sign up for a service" — it is "get my tips in before Thursday".

The unhappy version of the same moment: they open it on Sunday, mid-round, half the games already locked. Same flow, and it has to be honest about that too.

## 3. Goals

- A new player can go from a cold app to a submitted first tip in under 60 seconds, with no step that could have been removed.
- The player always knows how much of the process is left and can skip anything that is not essential.
- Under-18s are stopped at signup with a clear, kind message — never after they have invested time.
- No failure costs the player typed input or a made pick. Retry is always obvious.
- The flow ends on the real tipping screen, not a special first-run version of it.

## 4. Scope

**In**

- Welcome, age gate, email sign-up with a one-time code, display name, code preference, reminder permission, first tip.
- The sign-in path for players who already have an account.
- Every state and error in section 6.

**Out**

- Creating, joining or inviting anyone to a comp. The player tips in the default MberX Competition first.
- Mini games, currency and rewards.
- Passwords, social sign-in, SSO. Email only.
- Profile photos, avatars, or anything beyond a display name.
- Notification settings beyond the single permission ask.
- Ladders, results, comp sentiment — the onboarding exit is a tippable round, not a tour.
- Other sports or leagues.
- Payments, subscriptions, identity document checks.

## 5. Required functions

| # | What the player must be able to do | Why it matters |
|---|---|---|
| F1 | Understand what MberX is in one glance before giving anything away | Nobody hands over an email to a mystery |
| F2 | Confirm they are 18 or over, and see why we ask | The gate is at signup and must read as honesty, not a hurdle |
| F3 | Create an account with an email address | The only way in |
| F4 | Enter the one-time code we send, resend it, and recover from a wrong or expired one | Codes get mistyped and expire |
| F5 | Get back in if they already have an account | Returning players hit the same door |
| F6 | Choose the name their comp sees on the ladder | Ladders are people, not email addresses |
| F7 | Say which code they follow — AFL, NRL or both | Decides which round they land on |
| F8 | Choose whether to get reminders before lockout | The app owns reminders; permission is asked, never assumed |
| F9 | Skip anything optional and still reach tipping | Speed is the promise |
| F10 | See where they are in the process | Four steps with no map is a maze |
| F11 | Land on the current round and tip it | The entire point of the install |
| F12 | Know their first tip went through | Silent success reads as a failed tap |

## 6. States and edge cases

| State | When it happens | What the designer must show |
|---|---|---|
| First use | Cold app, nothing created | Welcome is the empty state — no form on it |
| Under 18 | Date of birth says under 18 | A kind block screen; no route forward, no scolding, no data kept |
| Invalid email | Malformed address | Inline error at the field; what they typed is kept |
| Email already registered | Sign-up with an existing email | Route to sign in instead — never a dead end |
| Account not found | Sign-in with an unknown email | Inline error, with a route to sign up |
| Sending code | Request in flight | Button in a working state, not frozen |
| Wrong code | Code mismatch | Inline error; the field is ready for another go |
| Expired code | Past its validity | Says it expired, and offers a new one |
| Resend cooldown | Within cooldown | Resend disabled with a countdown in plain words |
| Too many attempts | Rate limited | Says when to try again — a pause, not a wall |
| Verifying code | Check in flight | Working state before the next step appears |
| Network failure | Any request fails | Plain message and retry; typed input and made picks are kept |
| Name empty or invalid | Fails validation | Inline error with the rule stated (see section 10 — rules are open) |
| Name very long | Player types a long name | The field and every later use of the name cope gracefully |
| Notifications denied | OS permission refused, or "Not now" | Continues anyway; one line on turning reminders on later in Settings |
| Loading the round | Fetching fixtures | Skeleton list, not a bare spinner |
| No fixtures at all | Off-season, or a round not yet drawn | The designed empty state from the tipping brief; onboarding still completes |
| Round partly locked | Player arrives mid-round | Locked fixtures shown honestly (tipping brief); the open ones are still tippable |
| First tip submitted | After submit | Inline confirmation, with a little more warmth than the weekly version |
| Duplicate submit | Tapped twice on a flaky connection | One submission, no double record |

## 7. Recommended components

| Need | Recommended component or pattern | Reuse or new |
|---|---|---|
| Primary and secondary actions | HeroUI `Button` | Reuse |
| Email and display name entry | HeroUI `Input` (name confirmed at discovery) | Reuse |
| One-time code entry | Six-cell code field | **New** — check the library for an OTP or input-group first; custom only if none fits |
| Inline errors and notes | HeroUI `Alert` | Reuse |
| Step progress | A plain count — "Step 2 of 4" — or a step indicator | **New** — a count is acceptable; check `ProgressBar` before building |
| Code preference (AFL / NRL / Both) | HeroUI `ToggleButtonGroup`, three segments | Reuse — the library set carries a third toggle |
| Welcome and primer content blocks | HeroUI `Surface` | Reuse — `Surface` is the bare container; `Card` is a composed content card and misbehaves as a shell |
| Date of birth entry | Three `Input` fields (day / month / year) or one date field | Reuse — method is an open question (section 10) |
| Reminder primer | Full-screen step with one `Button` pair | Reuse |
| Fixture list, picks, submit, confirmation | Exactly as designed in `docs/briefs/tipping-brief.md` | Reuse that design — do not redesign it here |

Icons: HeroUI Icons first, Lucide only where HeroUI has no equivalent. Type: the HeroUI `Body` / `Heading` ramp.

## 8. Screens and flow

```
Welcome → Age gate → Email → Code → Display name → Code preference → Reminders → First tip → Submitted
                             ↘ Sign in (email → code) ↗
```

| Screen | Purpose |
|---|---|
| 01 Welcome | What MberX is, and the two doors: get started, or sign in |
| 02 Age gate | Confirm 18 or over before anything is collected |
| 03 Email | Enter an email address to create the account |
| 04 Code | Enter the one-time code, resend, recover |
| 05 Display name | The name the comp will see on the ladder |
| 06 Code preference | AFL, NRL or both — decides the landing round |
| 07 Reminders | Pre-permission primer for lockout reminders |
| 08 First tip | The current round, tippable — the exit of onboarding |
| 09 Submitted | First tip confirmed (a state of 08, per the tipping brief) |
| S1 Sign in | Email → code for existing players, rejoining at 08 |

Screens 06 and 07 are skippable ("Skip" / "Not now"); 02, 03, 04 and 05 are not. Frame naming follows the Tipping file convention: `OB / 01 Welcome`, `OB / 03 Email / error-invalid`, `OB / 08 First tip / 0 picked`, `OB / 08 First tip / submitted`.

If a state from section 6 needs its own surface, give it one rather than stacking modals.

## 9. Content and tone

- **Voice:** matey and brief. Australian English. Funny about football, never about money or someone losing.
- **Sentence case** for headings, labels and buttons. Full stops in helper text, none in one-sentence buttons.
- **Words to avoid:** odds, bet, punt, wager, stake, deposit, cash out, "free money", "guaranteed win", "risk-free", "beat the bookies", and anything that reads as a market or a promise of winning.

| Where | Copy |
|---|---|
| Welcome headline | Tipping, comps and mini games for your crew. |
| Welcome body | Tip the round with your mates and play for rewards between games. |
| Primary CTA | Get started |
| Secondary CTA | I've got an account |
| Age gate heading | First things first |
| Age gate body | MberX is 18 or over. Quick check before you get going. |
| Age gate CTA | Continue |
| Under 18 | Sorry — MberX is 18 and over. Come back when you're old enough. |
| Email heading | What's your email? |
| Email helper | We'll send a 6-digit code. No passwords here. |
| Email CTA | Send code |
| Code heading | Enter your code |
| Code helper | We sent a 6-digit code to {email}. |
| Code CTA | Continue |
| Wrong code | That code doesn't match. Have another go. |
| Expired code | That code's expired. Send a new one. |
| Resend | Resend code |
| Resend cooldown | Resend in 0:42 |
| Email already registered | That email's already got an account. Sign in instead. |
| Account not found | We can't find that one. Try again, or make an account. |
| Name heading | What should we call you? |
| Name helper | This is the name your comp sees on the ladder. |
| Code preference heading | Which footy do you follow? |
| Code preference helper | We'll land you on the right round. Switch any time. |
| Code preference options | AFL · NRL · Both |
| Reminders heading | Want a nudge before lockout? |
| Reminders body | Tips lock at kickoff. We'll ping you before the round closes — nothing else. |
| Reminders CTA | Turn on reminders |
| Reminders secondary | Not now |
| Notifications denied | No worries. You can turn reminders on in Settings any time. |
| Network failure | Didn't go through. Nothing's lost — try again. |
| Empty round | No games this round. Check back Thursday. |
| First tip submitted | Tips are in for Round 14. |
| First tip submitted (first run) | First tips are in. Welcome to MberX. |

Placeholders like `{email}` are placeholders, not final copy. Strings assume a one-time code; if passwords land instead, screen 04 changes and needs forgotten-password handling.

## 10. Constraints, decisions and open questions

**Constraints**

- Mobile first, one hand. 375 × 812 frames, matching the Tipping build.
- Dark theme only, with the dark mode set explicitly on every page and frame — the library collection defaults to light.
- WCAG 2.2 AA: 4.5:1 text contrast, 44px touch targets, visible focus, reduced-motion support.
- Email-only sign-in. No passwords, no social login in this flow.
- The age gate is at signup, before anything is collected.
- Times in AEST/AEDT (Sydney time); dates like `14 Nov 2026`.
- No new nav item, no new tab. Onboarding replaces the app chrome entirely.
- Screen 08 is the real tipping screen from the tipping brief — same layout, same copy rules. Do not invent a first-run variant.
- Compliance guardrails in `AGENTS.md` §6 apply to every string.

**Decisions**

| Question | Decision |
|---|---|
| Where does onboarding end? | First tip submitted. |
| Sign-in method | Email with a one-time code (user, 17 Nov 2026). |
| Is there a comp step? | No. The player is in the MberX Competition automatically and tips immediately. |
| Which steps are optional? | Code preference and reminders. Age gate, account and display name are not. |
| Which round does the player land on? | The current round of the code they follow; both codes default to AFL [assumed]. |

**Still open**

| Question | Who decides | What it blocks |
|---|---|---|
| One-time code or password? | Product | Whether screen 04 is a code field or a password field, and the forgot-password path |
| Age gate method: date of birth entry or self-declaration? | Product / legal review | The age gate screen itself |
| Under-18 handling: hard block or waitlist? | Product | The block screen's copy and exit |
| Display name rules: length, allowed characters, uniqueness, moderation | Product | Validation states on screen 05 |
| Is the code-preference step wanted at all? | Product | Whether screen 06 exists |
| What completes onboarding if no fixtures exist? | Product | The end state after the empty round |
| Should the first tip be tipped in AFL or NRL by default when the player follows both? | Product | The default landing code |

## 11. Build conventions (Figma)

Operational rules for the agent building this file. They come from `AGENTS.md` §10 and the lessons recorded in `docs/design/tipping-figma.md` — read that ledger before starting; its section 2 has the component keys.

- **One build owner, sequential, batched calls.** Figma MCP calls are metered (20/month on a Starter plan, 200/day on a Full seat). Do not fan out subagents into this file.
- **Discovery once.** One `search_design_system` batch for every component, variable and style; record the returned keys in a build ledger (`docs/design/onboarding-figma.md`) and never search again.
- **Library-first.** Compose from the attached design system [assumed: `MberX - Design System (HeroUI v3.0.5)` + Lucide Icons — verify at discovery]. A custom component that duplicates a library one is a defect; custom only when nothing fits, with the reason recorded.
- **Dark mode, explicitly.** Set the explicit variable mode on every page and frame. The collection default is light and will silently betray you.
- **`Surface` for bare containers.** `Card` is a composed content card; hiding its demo content hides its surface too.
- **Derive states by cloning.** Build one canonical frame per screen, clone and mutate per state. One component set per `use_figma` call.
- **Scripts must be safe to retry.** Check for an existing node by name before creating, so a retried call cannot duplicate nodes.
- **Evidence from the write.** Return node ids, counts and bounds from every write. Do not trust a text override or a variant picker without dumping what it wrote — that is where the Tipping build lost its budget.
- **Page structure:** `00 · Index`, `01 · Components`, `10 · Onboarding` with sections per flow stage, mirroring the Tipping file.
