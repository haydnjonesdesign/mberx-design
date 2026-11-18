# Tipping — UI/UX Design Brief

**Status:** Draft  
**Prepared:** 18 Nov 2026  
**Product / area:** MberX mobile app and web · AFL and NRL tipping  
**Design owner / stakeholders:** To confirm

> **Product constraints:** `AGENTS.md`  
> **Product model:** one master tipping card per code and round; every comp the player is in uses it. No per-comp tipping.

## 1. Outcome

- **What we are designing:** The AFL/NRL tipping experience from choosing a code and round through selecting and submitting tips, then checking lockout and results states — plus **Game Center**, a fixture-level screen that helps a player understand the match before tipping.
- **Desired user outcome:** A player can quickly tip open fixtures, see which picks are saved and locked, and understand results without entering tips again for each comp.
- **Why now / product context:** Weekly tipping is the core MberX loop. The screen needs to make the weekly task quick to complete and clear about what has been submitted, what is locked and what has resulted.
- **Scope:** The code switch, round context and navigation, fixture list, team and margin picks, submission feedback, lockout and results, byes and voids, post-lockout comp sentiment, access to comps, and Game Center for a fixture.
- **Game Center scope:** A fixture's team win/loss comparison, current injuries, and each team's ladder position, reachable from the fixture.
- **Out of scope:** Comp creation, joining and management; mini games, currency and rewards; other sports; draws as a pick, streaks, odds, prices, second scoring modes, editorial/news modules, play-by-play commentary, video, and notification settings beyond a reminder entry point.

## 2. Audience and user context

- **Primary audience:** The casual tipper, who opens the app once a week and may remember late; and the superfan, who wants every fixture and result.
- **Need / situation:** Most often, a player tips on a phone before the round gets underway. Sometimes they arrive after some fixtures have locked and need to know what remains possible. A player who wants context on a single match opens Game Center to weigh up the two teams before picking.
- **Secondary audiences or roles:** Players in the MberX Competition by default, and players who also belong to private or public comps. The tipping screen is the same for all of them.
- **Accessibility, device, or environment context:** Mobile-first and one-handed, with web as a wider view of the same product. Design for a player glancing at the screen between other activities.

## 3. Success criteria

| Criterion | How it will be observed | Source / status |
|---|---|---|
| A player can submit a full round in under 60 seconds from opening tipping | Usability test with a first-time player and a standard round | Product design goal |
| A player can tell which fixtures are open, locked, selected, live, or resulted | Ask the player to identify fixture state and next available action | Product requirement |
| A player knows whether a round is fully or partly tipped before submitting | Ask the player to describe remaining tips and submit consequences | Product requirement |
| A player completes a winner and margin pick for every selected fixture in the first and last rounds | Check first- and last-round designs for missing margin values before submission | Product requirement |
| A player understands one set of tips covers all their comps | Ask what happens to their other comps after they tip | Product requirement |
| Desktop and mobile show equivalent fixture and status information | Compare the same round and state at mobile and desktop widths | Product/design check |
| A player can open Game Center from a fixture and read both teams' win/loss, injuries and ladder position | Ask a player to assess a matchup from the screen alone | Product requirement |
| Opening Game Center does not slow tipping down | Time a player who opens it mid-round and returns to tip | Proposed design check |

## 4. Primary flow

1. Open tipping on the current round for the selected code.
2. Confirm the code, round, lockout context and how many fixtures need a tip.
3. Select a home or away team for each open fixture; change picks any time before that fixture's scheduled kickoff. In the first and last rounds, also enter the predicted winning margin in points for each fixture tipped. Open **Game Center** from a fixture to weigh the two teams up before picking.
4. Submit the current tips, whether partial or complete. In first and last rounds, a selected fixture's tip is complete only when its margin is entered. Submission is required before leaving the tipping screen or switching to the other code.
5. See confirmation and keep the submitted picks visible.
6. Return to the same round as fixtures lock and receive results. After the round locks, see comp tipping sentiment.
7. Continue to the player's comps when ready to check standings.

**Key branches or alternate paths:** Switching between AFL and NRL or leaving the screen with unsubmitted picks first requires submission of the current partial or complete tips. If submission fails, keep the player on the current screen with picks intact and a retry. After submission, a switch lands on the destination code's current round, not the same round number. Players may arrive after one or more fixture lockouts or encounter a bye, void or postponed fixture. Game Center is available from any fixture; returning from it restores the same round and any picks already made.

## 5. Screen inventory

| Order | Screen / view | User goal | Key information and actions | Entry / exit |
|---:|---|---|---|---|
| 1 | Tipping — open round | Tip fixtures that have not locked | AFL/NRL switch, current round, per-fixture kickoff and abbreviated team names, picks, first/last-round margin inputs, progress, submit | App navigation → submit or attempt to switch/leave |
| 2 | Tipping — partial round | Submit current tips before switching code or leaving | Locked fixtures remain visible; open fixtures remain selectable; partial count and submit action; margin input on first/last rounds | Same screen state; submission required before switch/leave |
| 3 | Tipping — submitted | Know the submission succeeded | Confirmation, round identity, submitted picks remain visible | Submission → same round |
| 4 | Tipping — locked / live | Review picks while games are underway | Locked state, live fixtures and picks; no unavailable editing controls | Lockout → results as they arrive |
| 5 | Tipping — results | Understand outcomes and points | Correct, incorrect, or void per fixture; reason for void; round result when complete | Results update in place; link to comps |
| 6 | Game Center | Understand the matchup before picking | Both teams with the win/loss comparison, current injuries, and ladder position; fixture identity and kickoff; back to the fixture | Fixture → back to the same round and picks |

The submitted, locked, live, and results views are states of the tipping screen, not separate destinations. Keep the fixture list as the source of truth for the round.

Game Center is a separate screen reached from a single fixture. It is reference material for the pick, not a place where the pick is made: the player returns to the fixture to tip. It carries no odds, prices or market-style presentation.

## 6. State coverage

| Screen / component | Relevant state | Expected user need / design response | Notes |
|---|---|---|---|
| Round | Loading | Show fixture-list loading structure | Avoid a lone indefinite spinner |
| Fixture | No pick / selected pick | Make both choices and the current pick unmistakable | Use the abbreviated team labels in section 8 |
| Round | Partly tipped | Show the count of selected and remaining open fixtures | Example: “3 of 8 picked”; distinguish locked-unpicked fixtures |
| First / last round fixture | Winner picked, margin missing | Make the required margin input clear and show which tip needs it | Do not supply a guessed or hidden default margin |
| First / last round fixture | Winner and margin picked | Keep the selected team and predicted margin together | Margin is a tie-breaker, not additional points |
| Submit | Partial or complete tips | Allow submission at any point; make clear what is being submitted | Each selected fixture in a first or last round needs both a team and margin; submission is required before leaving tipping or switching AFL/NRL |
| Navigation / code switch | Player tries to leave or switch with unsubmitted picks | Block the transition; offer “Submit tips” or “Keep tipping” | Do not discard picks or silently carry them to another code |
| Submit | Saving / success | Show progress, confirm the round and retain submitted picks | Submission confirmation is required |
| Submit | Network failure / duplicate tap | Preserve picks and offer a safe retry; only one submission is recorded | Retry must not create a second record |
| Fixture | Lockout passed, no pick | Say it is locked and that no tip was recorded | Lockout is at scheduled kickoff per fixture |
| Fixture | Correct / incorrect | Show result and scoring clearly | Scoring is flat: one point per correct tip; margin is used only as a tie-breaker in the first and last rounds |
| Fixture | Void / postponed / abandoned | State that there is no result, explain the reason when known, and clarify scoring | A void fixture scores nobody |
| Round | Bye | Identify the team and label the bye | Absence must not look like a missing fixture |
| Code switch | Different code has another round or lockout state | Show that code's current round and preserve its picks | No cross-code state or pick loss |
| Game Center | Loading | Show the matchup structure while data arrives | Avoid a lone spinner; keep the fixture identity visible |
| Game Center | Populated | Win/loss, injuries and ladder position for both teams, clearly attributed to each team | Use the abbreviations in section 8 |
| Game Center | Partial data (one team, no injuries, no ladder) | Show what is available and label the gap plainly | An empty injury list must read as "none listed", not as a loading failure |
| Game Center | Error / unavailable | Say the information is unavailable and offer a retry or a way back | Never block the player from tipping |
| Game Center | One team on a bye, or fixture void or postponed | Explain the fixture state instead of a matchup comparison | Keep the reason consistent with the fixture row |

## 7. Components and patterns

Use the MberX dark HeroUI design system described in `DESIGN.md`. Check the attached HeroUI library for each concept before creating custom patterns; name any library candidate checked and explain any mismatch in the design handoff.

| Pattern / component | Direction | Existing source or rationale | Design notes |
|---|---|---|---|
| Primary and secondary actions | Reuse | HeroUI `Button` | One clear primary submit action; retain disabled/loading feedback |
| Code switch | Adapt | HeroUI `ToggleButtonGroup`; use AFL and NRL only | Switching preserves picks and loads the other code's current round |
| Round navigation | Adapt | HeroUI buttons/select patterns; confirm best fit in library | Current round must be clear; avoid ambiguous previous-round score labels |
| Fixture and pick | New | No existing MberX fixture pattern identified | Two-way choice only; use the team abbreviations in section 8; kickoff and lockout state are visible |
| Picked / locked / result indicator | Adapt | HeroUI status and semantic tokens | Keep the state and available action clear |
| Round progress | New | No known existing pattern | Plain count of picked and remaining open fixtures |
| Margin pick | Adapt | Check HeroUI `Input` and number-entry patterns first | Required beside each selected fixture in the first and last rounds only; do not prefill a margin |
| Submit feedback | Adapt | HeroUI `Alert` / inline status pattern | Confirmation belongs near round context, not in a blocking modal |
| Bye row | Adapt | Fixture row, collapsed | Label the bye explicitly |
| Void result | Adapt | Status pattern with explanatory text | Give a reason where available; make clear nobody scores |
| Comp sentiment | New | No existing pattern identified | Percentages only, visible after lockout; no odds or market-style presentation |
| Game Center entry point | Adapt | Fixture row plus HeroUI `Button` / link candidate | A clear affordance per fixture that does not compete with the team picks |
| Matchup header | New | No existing MberX pattern | Both teams, fixture identity and kickoff; returns to the same round |
| Win/loss comparison | New | No existing pattern; check HeroUI data-display candidates first | Compare each team's record side by side; no odds, projections or "who wins" framing |
| Injury list | Adapt | HeroUI list / table candidate | Name, team and status per player; distinguish "none listed" from unavailable data |
| Ladder position | Adapt | HeroUI table/list or a compact stat block | Show each team's position and the ladder it comes from |
| Round/code explainer | Reuse / adapt | Existing help patterns to confirm | Keep rules concise and reachable without interrupting tipping |

Icons: HeroUI Icons first; Lucide only when HeroUI has no suitable icon.

## 8. Content language and tone

- **Language / locale:** Australian English. Dates use `14 Nov 2026`; times use AEST/AEDT (Sydney time).
- **Tone:** Matey, confident and brief. Football can be funny; never make fun of money or someone losing.
- **Terminology:** “Tip”, “fixture”, “round”, “lockout”, “Game Center”, “AFL”, “NRL”, “comp”. One set of tips serves every comp.
- **Content constraints:** Sentence case. Full stops in helper text; none in one-sentence buttons. Compliance guardrails in `AGENTS.md` apply.
- **Words to avoid:** odds, bet, punt, price, wager, stake, deposit, cash out, “free money”, “guaranteed win”, “beat the bookies”, and market language.
- **Illustrative copy:** “One set of tips. Every comp you're in gets them.” / “3 of 8 picked” / “Tips are in for Round 14.” / Game Center: “Last five” and “None listed” rather than “No injuries”.
- **Game Center language:** Describe teams and players factually. No odds, favouritism, “should win”, tips or predictions of the player's own pick.

Use the short team abbreviations in fixture labels, selection controls, byes and result summaries. The full names below define the mapping; do not substitute full names for the short labels in the tipping UI.

For each tip in the first and last rounds, ask the player to predict the winning margin in points as well as the winning team. The margin separates players tied on points; do not present it as an additional scoring point. Suggested label: “By how many points will {team} win?”

| Code | Team | Abbreviation |
|---|---|---|
| AFL | Adelaide Crows | ADEL |
| AFL | Brisbane Lions | BL |
| AFL | Carlton | CARL |
| AFL | Collingwood | COLL |
| AFL | Essendon | ESS |
| AFL | Fremantle | FRE |
| AFL | Geelong Cats | GEEL |
| AFL | Gold Coast Suns | GCFC |
| AFL | GWS Giants | GWS |
| AFL | Hawthorn | HAW |
| AFL | Melbourne | MELB |
| AFL | North Melbourne | NMFC |
| AFL | Port Adelaide | PORT |
| AFL | Richmond | RICH |
| AFL | St Kilda | STK |
| AFL | Sydney Swans | SYD |
| AFL | West Coast Eagles | WCE |
| AFL | Western Bulldogs | WB |
| NRL | Brisbane Broncos | BRI |
| NRL | Canberra Raiders | CBR |
| NRL | Canterbury-Bankstown Bulldogs | CBY |
| NRL | Cronulla-Sutherland Sharks | CRO |
| NRL | Dolphins | DOL |
| NRL | Gold Coast Titans | GLD |
| NRL | Manly Warringah Sea Eagles | MAN |
| NRL | Melbourne Storm | MEL |
| NRL | Newcastle Knights | NEW |
| NRL | New Zealand Warriors | WAR |
| NRL | North Queensland Cowboys | NQL |
| NRL | Parramatta Eels | PAR |
| NRL | Penrith Panthers | PEN |
| NRL | South Sydney Rabbitohs | SOU |
| NRL | St George Illawarra Dragons | STI |
| NRL | Sydney Roosters | SYD |
| NRL | Wests Tigers | WST |

The AFL abbreviations are the official 2026 AFL ladder-feed values. NRL does not publish a canonical abbreviation list in the cited material; its short labels above are common scoreboard codes. Treat these as display labels, not identifiers, and confirm NRL labels against MberX's chosen sports-data provider before implementation. Team sets reflect the 2026 men's competitions (18 AFL, 17 NRL); future expansion or provider changes may change them.

Sources: [AFL 2026 ladder feed](https://aflapi.afl.com.au/afl/v2/compseasons/85/ladders?roundId=1367) and [AFL teams](https://www.afl.com.au/teams); [NRL clubs](https://www.nrl.com/clubs/) and [Fox Sports NRL match centre](https://www.foxsports.com.au/nrl/nrl-premiership/match-centre/NRL20250103/match-report) for scoreboard short-code usage.

## 9. Design-system requirements

- Treat the attached libraries as the source of truth.
- Search the libraries before creating custom UI elements.
- Use linked library instances for Button, Input, InputOTP, ProgressBar, Checkbox, and other suitable components.
- Use the library’s semantic color, spacing, radius, typography, and effect variables and styles.
- Do not hardcode values when a suitable token exists.
- Use published heading styles according to their intended hierarchy, with only one Heading 1 per screen.
- Keep component instances linked; do not detach or manually recreate available components.
- Use Auto Layout throughout and give frames and important layers clear semantic names.
- When components are not available in a library, create them in this file.

## 10. Constraints, dependencies, and open questions

- **Constraints / non-negotiables:**
  - AFL and NRL only; two-way tips, no draw pick.
  - One point per correct tip; scoring is not recalculated in the client.
  - First and last rounds require a predicted winning margin in points alongside each fixture tip; margins break ties and do not add points.
  - One master card per code and round, shared by every comp.
  - Each fixture locks at scheduled kickoff; store UTC and show Sydney time.
  - Round contains 8 fixtures. Use the abbreviations in section 8 for team labels.
  - Void fixtures score nobody. Show comp tipping percentages only after round lockout.
  - Mobile first and one-handed; web is a wider view of the same tipping experience.
  - No extra navigation item or news carousel inside the task.
  - Game Center is informational only: win/loss comparison, injuries and ladder position. No odds, prices, predictions, commentary, video or market-style framing.
  - Game Center never blocks tipping. A missing or failed data source leaves the fixture pickable.
- **Dependencies:** Fixture, lockout, result and scoring data must come from the product's single source of truth. Game Center adds win/loss records, injury data and ladder position, so those feeds need a source and an update cadence. No stack or implementation choices are specified here.
- **Open questions:**

| Question | Who / what resolves it | What it blocks |
|---|---|---|
| When a fixture finishes level, how is a two-way tip scored? | Product | Drawn-match result state and copy |
| What counts as a void or postponed fixture, and when is that decision final? | Product / sports data | Void state and result timing |
| What exact margin comparison breaks a tie, and how are equal margin guesses ranked? | Product | Margin result states and explanation |
| What margin value range is valid for an AFL or NRL fixture? | Product / sports data | Margin field validation |
| Which win/loss window does Game Center compare — season record, recent form, or head-to-head? | Product / sports data | Comparison design and its labels |
| Which ladder does Game Center show — the league ladder, or the player's comp ladder? | Product | Ladder block design and copy |
| What injury detail is shown, and how current must it be? | Product / sports data | Injury list fields, empty state and “as at” labelling |
| Is Game Center reachable from every fixture state, or only before lockout? | Product | Entry point placement and locked-fixture behaviour |

- **Assumptions:** Team abbreviations in section 8 are display labels. Confirm them against the chosen sports-data provider before implementation.

## 11. Figma file organisation and handoff

Recommended page structure; verify the target Figma file before starting.

1. **Page: `00 Index`** — cover art only.
2. **Page: `01 Components`** — shared tipping patterns, fixture state examples and Game Center blocks, composed from HeroUI where suitable.
3. **Page: `02 Mobile`** —  ordered open-round flow, Game Center, then locked, results and error states.
4. **Page: `03 Web`** —  ordered open-round flow, Game Center, then locked, results and error states.

- **Frame ordering:** Match the primary flow. Name frames `[flow] / [order] [view] / [state]`, for example `TIP / 01 Open / AFL`, `TIP / 01 Open / partial`, `TIP / 02 Submitted`, `TIP / 03 Locked`, `TIP / 04 Results`, `GC / 01 Matchup / Populated`, `GC / 01 Matchup / Partial data`.
- **Responsive/platform variants:** The Mobile page uses a 375 × 812 working viewport; the Desktop page shows the wider web view. Keep fixture, round and status information available in both.
- **Existing conventions to follow:** Explicit dark mode on every page/frame; HeroUI library-first; Lucide Icons first; follow the available MberX design-system guidance.
- **Review / handoff expectation:** Final frames cover the primary path and named states in section 6, including Game Center in its populated, partial-data and unavailable states. Call out the unresolved drawn-match scoring rule and the open Game Center data questions rather than designing around an assumed answer.

## 12. Review checklist

- [ ] AFL and NRL have independent picks and each switch lands on that code's current round.
- [ ] The comp relationship is clear without a comp picker or duplicate per-comp tipping.
- [ ] Open, selected, locked, live, correct, incorrect and void states and their available actions are clear.
- [ ] First and last rounds require an explicit margin pick for every selected fixture, with no prefilled guess.
- [ ] Progress and partial submission are understandable before the player submits.
- [ ] The design includes success, failure/retry and bye states.
- [ ] Game Center is reachable from a fixture, shows both teams' win/loss, injuries and ladder position, and returns to the same round with picks intact.
- [ ] Game Center handles partial data, an empty injury list and unavailable data without blocking the tip.
- [ ] Game Center uses no odds, predictions, favouritism or market framing.
- [ ] No odds, market language, draw option or second mode is included.
- [ ] Mobile and web expose equivalent essential fixture and round information.
- [ ] Existing HeroUI patterns are reused or adaptation/new work is explained.
- [ ] Dark theme and Sydney time are reflected.
- [ ] The draw-result rule remains an explicit product question until decided.
