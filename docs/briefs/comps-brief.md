# Comps — Design Brief

> **For:** designer · **Status:** draft · **Date:** 18 Nov 2026
> **Evidence:** `ux-audit/espn-footytips/competitions/espn-footytips-competitions-ux-spec.md` (reference product) + `AGENTS.md` + `docs/briefs/tipping-brief.md`
> **Model:** comps consume the master tipping card. A comp is a ladder and a crew, not a second place to enter tips.
> **Derived, not copied:** the reference product is comp-centric and multi-sport, with three game modes and a betting-odds mode. MberX is code-centric, two codes, one scoring model. The structure below keeps what the reference proved and drops what does not survive that change. See the appendix for the specific keeps and drops.

## 1. Snapshot

A player creates a comp, names it, and invites their crew. Everyone in it tips the round once — the same master card they use in every other comp — and the comp ranks them on its own ladder. This brief covers the whole comps area: the list of comps a player belongs to, starting a comp, joining one, and the comp itself (ladder, members, invite, wall, settings). Tipping is designed elsewhere and is not re-specified here.

The default MberX Competition is a comp like any other in the list. It is the floor of the product: every player is in it before they ever join anything, so the list has to look complete when it holds exactly one comp.

## 2. The moment

**The captain, Thursday afternoon.** They've been talking up a comp in the group chat for a week. They are on their phone, between things, and want it done before the first bounce: name it, get the link, paste it into the chat. If starting a comp takes more than a minute they will do it next week, which means never.

**The player, Sunday night.** Results are in. They open the app to see whether they're still top of the crew and whether Dave, who talks a lot, is last. They read the ladder, maybe post one line, and close it. This is the loop's reward and it has to be readable in five seconds on a phone.

**The invitee, whenever.** A mate sends a link. They tap it, see a comp with a name and some people they know, and join — or they bounce, because a join screen that asks for a password is a wall.

## 3. Goals

- A captain can go from "no comp" to "link in the group chat" in under a minute.
- A player can see where they stand in every comp they're in without opening any of them.
- A player can read the full ladder on a phone, including round-by-round, with no horizontal guesswork and no missing columns.
- An invitee can tell what they're joining, and who else is in it, before they commit.
- Nobody can accidentally leave a comp, and nobody can accidentally change one.
- A player never wonders whether they need to tip again for a particular comp.

## 4. Scope

**In**

- The list of comps a player belongs to, including the default MberX Competition.
- Starting a comp: name, who can join, and the invite link.
- Joining: by link, by join code, and by finding a public comp.
- The comp itself: ladder, members, invite, wall, settings.
- Admin (captain) actions: rename, change who can join, rotate the join code.
- Leaving a comp, and what a member sees when they can't change something.
- Every state and edge case in section 6.

**Out**

- Entering tips. The tipping screen owns that, and the comp never asks for a comp-specific tip.
- Game modes. Tipping is the only mode. No streak mode, no odds-based mode, no second scoring model.
- Custom scoring. One point per correct tip, flat, both codes. There is no scoring editor.
- Entry fees, prizes, buy-ins, or any comp-level money. MberX is not a betting product and prize draws are a separate, regulated surface.
- Choosing sports. MberX has AFL and NRL; a comp does not pick from a catalogue of leagues.
- Comp pictures and uploads. A comp is identified by its name and a generated crest.
- Season rollover, archiving, renewing a comp for a new season.
- Admin transfer, member removal, join requests and approvals.
- Reactions, threads, mentions and notifications on the wall. Plain posts only.
- Comp analytics, exports, and any report beyond the ladder itself.
- Mini games, currency and rewards.

## 5. Required functions

Ordered by the journey: find your comps, start one, join one, live in one.

| # | What the player must be able to do | Why it matters |
|---|---|---|
| F1 | See every comp they're in, in one list, with the MberX Competition among them | This is the home of the social half of the product |
| F2 | See their standing in each comp without opening it | "Where am I?" is the reason they opened the app |
| F3 | Tell which comp needs them this round, and which is already locked | A locked comp and an open one look identical today |
| F4 | Open a comp and land on its ladder | The ladder is the comp's home, not a sub-tab |
| F5 | Switch between AFL and NRL inside a comp | Tips are per code, so standings are per code |
| F6 | Start a comp and name it | The only setup step that matters |
| F7 | Choose who can join: anyone, anyone with the link, or invite only | Openness is the captain's call, and it changes the join path |
| F8 | Get a shareable link the moment the comp exists | The comp is useless until the link is in the chat |
| F9 | Share that link through their phone's normal share sheet, or copy it | Pasting into a group chat is the actual distribution |
| F10 | Join a comp from a link, and see what they're joining first | Blind joins into the wrong comp are common |
| F11 | Join a private comp with a join code | Some crews don't want a link floating around |
| F12 | Find and join a public comp | Players with no crew still need a ladder |
| F13 | Read the ladder: rank, player, this round, season total | The core object of the screen |
| F14 | Find themselves on the ladder without scanning for their own name | Self-location is the first thing they look for |
| F15 | See round-by-round scores for the season, on a phone | The reference dropped these entirely on mobile |
| F16 | Understand what a round column means, and when it locked | Round codes without a legend are a puzzle |
| F17 | See who's in the comp, and who runs it | The roster is how you check your mates joined |
| F18 | Invite more people later, without hunting for the original link | Comps grow after they're made |
| F19 | Post a message to the comp | Banter is half the loop |
| F20 | Read what others have posted, with who said it and when | A wall with no names and no times is noise |
| F21 | Understand how this comp scores and when tips lock, in one line | "How do I win this?" should never need a support ticket |
| F22 | Leave a comp, deliberately, and know what leaving costs | The only destructive action in the area |
| F23 | As captain, rename the comp and change who can join | The name is wrong the moment the comp is real |
| F24 | As captain, rotate the join code when it leaks | A leaked code is the failure mode of invite-only |
| F25 | As a member, tell the difference between "read only" and "you can't" | Silent read-only reads as a broken app |

## 6. States and edge cases

| State | When it happens | What the designer must show |
|---|---|---|
| Only the MberX Competition | New player, no private comps | A designed list of one, with starting and joining as the obvious next move — not an empty screen |
| No comps at all | Membership data failed to load | An error with a retry, never a bare empty list |
| Many comps | 12+ comps | A sensible ordering, and the list stays scannable |
| Round open, nothing tipped | The weekly default | The card says tips are open, and how many are left |
| Round locked, tips in | After kickoff | The card says locked, and the points are pending, not zero |
| Round resulted | Results in | This round's points, and rank movement |
| Round void or partial | Postponed fixtures | Points pending with a reason, not a silent zero |
| Comp with one member | Captain just made it | The ladder of one, plus the invite action front and centre |
| Comp with no scores yet | Before the first result | "Nothing to rank yet" with the next lockout — not a table of zeros |
| Long comp name | 40 characters, or a name with emoji | The card, the ladder header and the invite all cope |
| Very long player name | 30 characters | Ladder rows and member rows don't break |
| Large comp | 100+ members | Pagination or a "show more" that is honest about how many are hidden |
| Comp full | Size limit reached, if one exists | Says full, and says what to do about it |
| Invite link opened, already a member | Tapped their own link | Goes to the comp, with a line saying they're already in |
| Invite link opened, comp at capacity | Full comp, new player | A clear refusal, no dead-end tap |
| Join code wrong | Typo, or rotated code | Inline error, code field keeps its place |
| Join code correct, comp gone | Comp deleted between send and tap | "That comp's not here any more", with a way back |
| Link expired or rotated | Old link after a rotation | Says the link is old, and offers the code path |
| Public comp search, no results | Nothing matches the query | An honest empty state, with a route to start your own |
| Public comp search, nothing public yet | Cold market | Not a broken screen — an explanation and the create path |
| Leaving a comp | Member taps leave | Confirmation that names the comp and says tips are unaffected |
| Last member leaves | Captain abandons | Comp is not left orphaned — see section 10 |
| Captain leaves | Admin taps leave | Blocked or handed over — see section 10 |
| Member views settings | Non-captain opens settings | Read-only fields that look read-only, with one line saying who can change them |
| Captain views settings | Captain opens settings | Editable, with a save that confirms |
| Network failure | Any request fails | Plain message, retry, nothing typed is lost |
| Duplicate submit | Double tap on a flaky connection | One comp created, one post, one join — never two |
| Wall with no posts | New comp | An invitation to post first, not a moderation warning |
| Wall post fails | Send fails | The text stays in the composer |
| Wall post very long | Player pastes an essay | A stated limit, and the counter appears before they hit it |
| Wall content reported or removed | Moderation action | Removed post shows as removed, with who removed it |
| Comp not found | Bad or old link | One honest screen, with a route to their comps |
| Both codes, one comp | AFL resulted, NRL still open | Each code carries its own state; no cross-talk |

## 7. Recommended components

Check the HeroUI library before building anything marked **New**. A custom component that duplicates a library one is a defect.

| Need | Recommended component or pattern | Reuse or new |
|---|---|---|
| Comp list container | A stack of comp cards on the canvas, not nested cards | Reuse `Surface` |
| Comp card | One card per comp: crest, name, member count, one row per code with rank and total, and a state line | **New** — the core component of this area |
| Comp crest | Generated from the comp name — initials in a stable colour | **New** — no uploads in v1 |
| Standing row inside a card | Code label, rank, total, and a movement indicator that is not colour alone | **New** — pair the triangle with a signed number |
| Round state line | One line: open with a count left, locked with the time, or resulted with points | Reuse status chip plus text |
| Shared round summary | One line above the list, because this round's points are identical in every comp | **New** — stops the same number repeating per card |
| Empty list state | Centred block with the two doors: start a comp, join with a code | **New** |
| Start a comp form | One screen, three fields, one primary action | Reuse `Input`, `ToggleButtonGroup`, `Button` |
| Who can join | Three-segment control: anyone, anyone with the link, invite only | Reuse `ToggleButtonGroup` |
| Invite link row | The link, truncated in the middle, with copy and share | **New** — the highest-value control in the area |
| Share | The OS share sheet, opened from one button | **New** — platform behaviour, not a custom menu |
| Join preview | Comp name, crest, captain, member count, and a join button | **New** — prevents blind joins |
| Join code entry | One short code field, auto-advancing, with paste support | **New** — check the library for an OTP-style field first |
| Public comp results | A list of comp rows with name, member count and join | Reuse list pattern from members |
| Comp shell | Header with crest, name and a switch for AFL/NRL, then tabs | **New** — build once, reuse on all five tabs |
| Tabs | Ladder, members, invite, wall, settings — horizontally scrollable, never clipped | Reuse `Tabs` |
| Ladder, desktop | Table with a sticky player column and one column per round | Reuse `Table` |
| Ladder, mobile | Rank, player, this round, total; round history behind a row tap | **New** — the reference dropped 18 columns and said nothing |
| You marker | A "You" chip pinned on the player's own row, plus a way to jump to it | **New** — solves self-location without a search field |
| Round label | Plain words — "Round 14", "Grand Final" — never bare codes | Reuse text style |
| Member row | Avatar, name, captain chip, and this round's points | Reuse list row |
| Invite surface | Link first, email second, both on one screen with the link given priority | **New** |
| Wall composer | Avatar, text field, post button that enables on content | Reuse `Input` + `Button` |
| Wall post | Author, relative time, body, and a quiet overflow for report | **New** |
| Settings panels | Grouped fields with an explicit read-only treatment for members | Reuse `Surface` + `Input` |
| Leave comp | Destructive action, isolated at the foot of settings | Reuse `Button / Danger` |
| Leave confirmation | Modal naming the comp and what is unaffected | Reuse `Modal` |
| Notices | Inline notices for locked, full, gone, and read-only | Reuse `Alert` |

Icons: HeroUI Icons first, Lucide only where HeroUI has no equivalent.

## 8. Screens and flow

```
Your comps ──┬─→ Comp ─→ Ladder ─┬─→ round detail (mobile)
             │                   ├─→ Members
             │                   ├─→ Invite ─→ share sheet / copy
             │                   ├─→ Wall
             │                   └─→ Settings ─→ Leave comp (confirm)
             ├─→ Start a comp ─→ Comp created ─→ Invite
             ├─→ Join (link) ─→ Join preview ─→ Comp
             ├─→ Join (code) ─→ Comp
             └─→ Find a comp ─→ Join preview ─→ Comp
```

| Screen | Purpose |
|---|---|
| 01 Your comps | Every comp, with standings, and the two ways in |
| 02 Start a comp | Name it, choose who can join, create |
| 03 Comp created | Confirmation that leads straight into inviting |
| 04 Join a comp | Link, code, or find — one screen, three routes |
| 05 Join preview | What you're joining, before you commit |
| 06 Find a comp | Public comps, searchable |
| 07 Comp — Ladder | The comp's home: standings per code |
| 08 Comp — Round detail | One player's round history, or one round's scores (mobile) |
| 09 Comp — Members | The roster |
| 10 Comp — Invite | Link, share, email |
| 11 Comp — Wall | The comp's message board |
| 12 Comp — Settings | Name, access, join code, scoring, leave |
| 13 Comp not found | The dead-link state |

Screens 07–12 share the comp shell: crest, name, AFL/NRL switch, tabs. States from section 6 are frames of these screens, not new destinations — except 13, which is its own screen because there is no comp to wrap it in.

Frame naming follows the Tipping convention: `CMP / 01 Your comps`, `CMP / 01 Your comps / empty`, `CMP / 07 Ladder / no scores`, `CMP / 07 Ladder / mobile`.

## 9. Content and tone

- **Voice:** matey and brief. Australian English. Funny about football, never about money or someone losing.
- **One word for one thing.** It is a **comp**, always — never "competition", "league", "group" or "pool". The area is **Comps**.
- **Sentence case** for headings, labels and buttons. Full stops in helper text, none in one-sentence buttons.
- **Words to avoid:** odds, bet, punt, wager, stake, deposit, cash out, prize pool, "free money", "guaranteed", "beat the boys". A comp is a ladder, not a market.
- Losing a round is a joke. Never joke about money or about someone being excluded.

| Where | Copy |
|---|---|
| Comps heading | Your comps |
| Comps subline | One set of tips. Every comp you're in gets them. |
| Shared round line | Round 14 · 5 of 8 correct · locked 7:40 pm |
| Card, open round | Tips open · 3 left |
| Card, locked | Locked · 7:40 pm |
| Card, resulted | +5 this round |
| Empty list | You're in the MberX Competition. Get your crew in too. |
| Empty list CTAs | Start a comp · Join with a code |
| Start a comp heading | Start a comp |
| Name label | Comp name |
| Name helper | This is what your crew sees on the ladder. |
| Name placeholder | Thursday Night Crew |
| Who can join label | Who can join? |
| Who can join options | Anyone · Anyone with the link · Invite only |
| Who can join helper | You can change this later. |
| Create CTA | Create comp |
| Comp created heading | Comp's up. |
| Comp created body | Send the link to your crew. Everyone who joins gets the same ladder. |
| Invite link action | Copy link |
| Invite link secondary | Share |
| Copied | Link copied. |
| Join screen heading | Got a comp to join? |
| Join code label | Join code |
| Join code helper | Six letters, from whoever invited you. |
| Find a comp | Find a comp |
| Find a comp empty | No comps match that. Try a different name, or start your own. |
| Find a comp, cold | No public comps yet. Start one and be first. |
| Join preview | You're invited to {comp} |
| Join preview meta | {n} players · started by {captain} |
| Join CTA | Join comp |
| Already a member | You're already in {comp}. |
| Comp full | This comp's full. |
| Wrong code | That code doesn't match. Check it with whoever invited you. |
| Link rotated | That link's out of date. Ask for the new one, or use the join code. |
| Comp gone | That comp's not here any more. |
| Ladder, no scores | Nothing to rank yet. Scores land after the first round. |
| Ladder, you chip | You |
| Ladder, empty round | No games this round. |
| Members heading | Members |
| Members meta | {n} in the comp |
| Members search | Search by name |
| Captain chip | Captain |
| Invite heading | Invite your crew |
| Invite email label | Invite by email |
| Invite send | Send invite |
| Invite sent | Invite sent to {email}. |
| Wall heading | Wall |
| Wall composer | Say something to the crew… |
| Wall post CTA | Post |
| Wall empty | Nothing on the wall yet. Get in first. |
| Wall failed | Didn't post. Your message is still here — try again. |
| Settings heading | Comp settings |
| Settings, member view | Only {captain} can change these. |
| Scoring line | One point per correct tip. Tips lock at kickoff. |
| Rotate code | New code |
| Rotate code confirm | Get a new code? The old one stops working. |
| Leave comp | Leave comp |
| Leave confirm heading | Leave {comp}? |
| Leave confirm body | Your tips aren't affected — you're still in every other comp. You can rejoin with the link. |
| Leave confirm CTA | Leave comp |
| Leave confirm cancel | Stay |
| Network failure | Didn't go through. Nothing's lost — try again. |
| Comp not found | We can't find that comp. The link might be old, or the comp's gone. |

`{comp}`, `{n}`, `{captain}` and `{email}` are placeholders. Every string here is a proposal, not final copy.

## 10. Constraints, decisions and open questions

**Constraints**

- Mobile first, one hand. 375 × 812 frames, matching the Tipping build. The ladder must be readable at that width without horizontal scrolling of the whole page.
- Dark theme only, with the dark mode set explicitly on every page and frame.
- WCAG 2.2 AA: 4.5:1 contrast, 44px targets, visible focus, reduced motion. Rank movement, round state and the you-marker must never rely on colour alone.
- Tips are code-scoped. A comp never asks which comp to tip for, and never shows a comp-specific tip entry point.
- Scoring is displayed, never recalculated in the client. One point per correct tip, both codes.
- A comp spans both codes, with one ladder per code and a switch on the ladder `[assumed]` — see open questions.
- Round labels are plain words. "Round 14", "Grand Final". No `WC`, `FW1`, `SF`, `PF` codes.
- Times in AEST/AEDT (Sydney time); dates like `14 Nov 2026`.
- No new nav item beyond the Comps destination itself. Inside a comp, navigation is tabs.
- No entry fee, no prizes, no odds, no wagering language anywhere in the area.
- Every destructive action is confirmed. Every read-only state says why.
- The wall is plain text. No reactions, no threads, no notifications in v1.

**Decisions**

| Question | Decision |
|---|---|
| Is a comp a second place to tip? | No. One master card per code serves every comp. |
| How many game modes? | One. Tipping. No streak, no odds mode. |
| Custom scoring? | No. Flat one point per correct tip. |
| Which sports can a comp cover? | AFL and NRL only, both, with a ladder per code `[assumed]`. |
| How many steps to start a comp? | One screen. Name, who can join, create. |
| How is a comp identified visually? | Name plus a crest generated from the name. No uploads in v1. |
| How does an invite travel? | A link, shared through the OS share sheet. Code as the fallback for invite-only comps. |
| Can a member see the join code? | Yes, only if they're in the comp. It is never printed on a public screen. |
| Is the ladder the comp's landing tab? | Yes. |
| Where does leaving live? | Settings, at the foot, isolated and confirmed. Never beside a constructive action. |
| Can a member edit comp settings? | No. Fields read as read-only with one line naming the captain. |
| What happens to a comp's rounds before any result? | An empty state with the next lockout, not a table of zeros. |
| What is the longest comp name to design against? | 40 characters. Longest player name: 30. `[assumed]` |
| Largest comp to design against? | 100 members, paginated. `[assumed]` |

**Still open**

| Question | Who decides | What it blocks |
|---|---|---|
| Does a comp cover both codes, or does the captain pick one at creation? | Product | The create form, the ladder's code switch, and every card's standing rows |
| Is there a comp size limit, and what happens at it? | Product | The full-comp state and the join preview |
| What happens when the captain leaves — blocked, or handed to the next member? | Product | The captain's leave path and the orphaned-comp state |
| Can a comp exist with zero members after everyone leaves? | Product | The last-member-leaves state |
| Do public comps appear in a browsable list, and in what order? | Product | Whether screen 06 exists as a list or just a search field |
| Is the wall moderated in-product, and who can remove a post? | Product / moderation | The wall's overflow menu and the removed-post state |
| Does an invite email get sent, and from where? | Engineering / product | Whether the email route on screen 10 is real or link-only in v1 |
| Can the join code be rotated, and does rotating kill old links? | Product | The rotate control and the rotated-link state |
| Is there a season boundary, and does a comp carry across it? | Product | The ladder's round range and any "season" label |
| What does a new player see if the MberX Competition has no results yet? | Product | The list's cold state |

## Appendix — what the reference product got right and wrong

From the ESPN FootyTips competitions audit. Take the pattern, not the page.

**Worth keeping**

- One list holding every comp, with standings legible without opening anything.
- The global comp presented as just another comp in that list, with population-scale ranks.
- Name, who can join, and an invite link collected together at creation — the comp is only useful once the link is out.
- Each option in a creation flow carrying a one-line explanation of what it does.
- A comp shell with tabs, where the tab is in the URL so it survives a refresh and can be shared.
- A roster with a captain chip and a search field.
- A wall composer that is a single field and a single button.
- An invite message prefilled and editable by the sender.

**Worth avoiding**

- Four-step creation for three decisions, two of which are single Yes/No questions. One screen.
- Sports multi-select across 14 leagues. MberX has two codes and the comp doesn't choose.
- A betting-odds game mode inside a creation flow aimed at casual players.
- Per-comp round scores on every card when the tips are shared — the same number repeated, and two near-identical labels ("Round Rank" vs "Comp Rank") meaning different things.
- An 18-column ladder on desktop that drops to 4 columns on mobile with no notice, no scroll and no per-round view.
- A ladder showing 10 of 25 members with nothing saying so.
- Round codes with no legend.
- A destructive "Leave" control sitting in the same row, same weight and same position as 24 "Send Message" buttons, on the player's own row, with no confirmation.
- Read-only settings rendered as plain text, so nothing is focusable and nothing announces why it can't be changed.
- A private comp's password printed in cleartext to every member who opens settings.
- A search-and-join screen that renders nothing by default, leaving "start your own" as the only visible action.
- No empty state on the wall, so the only guidance on screen is a moderation warning.
- One consent question stated three times in three voices, as a segmented toggle.
- Four different labels for the same action, including one misspelling.
- A news carousel and a repeated league-ladder widget inside the comp surfaces.
