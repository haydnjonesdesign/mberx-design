# Competitions — UI/UX Design Brief

**Status:** Draft  
**Prepared:** 18 Nov 2026  
**Product / area:** MberX mobile app and web · competitions  
**Design owner / stakeholders:** To confirm

> **Product constraints:** `AGENTS.md`  
> **Inspiration, not a specification:** `docs/ux-audit/espn-footytips/competitions/espn-footytips-competitions-ux-spec.md`. Reuse the principles, not the feature set or the visuals.

## 1. Outcome

- **What we are designing:** Seeing and searching comps, creating and managing public or private comps, joining by invitation or discovery, and the comp landing screen that carries the comp's identity, standings, members, statistics, and its optional Chat, branding and rewards.
- **Desired user outcome:** A player gets into the right comp, brings their crew in, and sees where they stand without leaving the comp to find the ladder, the members or the banter.
- **Why now:** Comps are the social layer of the weekly tipping loop. Every player already has the default MberX Competition; private comps and public/private joining extend it.
- **Scope:** My comps with in-place search; comp creation and joining; the comp landing screen (title, branding, ladder, members, statistics widget, Chat); comp settings with member management and on/off settings for Chat, branding and rewards; invitation URLs and sent/joined statuses; ladder movement; Chat with text, image and emoji posts and captain post removal; captain-entered reward text; season score reset; mobile and web.
- **Out of scope:** New sports or game modes; Flexi/Streak or odds-based scoring; paid entries; a reward catalogue, reward selection from the MberX reward programme, or in-app fulfilment; DMs, reactions, chat notifications; back-office tools.

The ESPN audit shows players benefit from an at-a-glance view across comps, a clear creation sequence and a consistent comp context. Do not copy its per-comp tipping model, game modes, fees, ads, sport catalogue or navigation.

## 2. Audience and user context

- **Primary audience:** The captain, who creates and manages a comp, invites their crew and wants control and visibility. The casual tipper, who wants to find their comp and see how they are tracking.
- **Need / situation:** A captain configures a comp, shares an invitation link and manages settings and Chat. A player searches for a public comp, accepts a pending private invitation on My comps without a PIN, or follows an invitation link and enters the PIN. Then they check the ladder.
- **Current behaviour or pain point:** MberX's model includes a default MberX Competition, public/private comps, invites and ladders. The screens and interaction rules for the expanded management experience are not specified. Treat the ESPN audit as reference only, not as evidence of MberX behaviour.
- **Secondary audiences:** The superfan, who wants ladder context without clutter. The reward hunter, who needs the assigned reward and its round to be clear without the comp becoming a shopfront.
- **Accessibility, device, environment:** Mobile-first, one-handed. Web is a wider view of the same product. Keep names, standings, membership and key actions clear at both sizes. Do not claim a formal WCAG level.

## 3. Success criteria

| Criterion | How it will be observed | Source / status |
|---|---|---|
| A player can name their comps, including the default MberX Competition | Ask them to identify their comps and the default one | Product requirement |
| A captain can create a comp and find the next step to bring players in | Unassisted creation-to-invitation prototype task | Product capability; flow details To confirm |
| A player knows Accept on My comps needs no PIN, and the link always does | Ask what they would do for each entry point | Product rule |
| A player can see a pending invitation on My comps and accept it there | Give a pending invitation; ask them to join without the original message | Product requirement |
| A captain can explain the two auto-tip options and when the code and rule lock | Ask what they can still change after the first match starts | Product rule |
| Players can explain ladder ranking and identify their own movement | Rank sample tipsters; describe their own movement | Product rule |
| A player can tell which reward belongs to which placing and round | Interpret a sample reward schedule | Product capability |
| A player knows leaving removes their tips and reward eligibility | Ask what happens if they leave | Product rule |
| A player knows one set of tips covers every comp | Ask what happens to their other comps after tipping | Product requirement |
| A player can find their standing, the members and Chat on the landing screen at both widths | Locate each section and their own row without leaving the screen | Design check; movement period To confirm |
| A captain can invite and remove members without leaving the comp | Ask a captain to invite one player and remove another | Product requirement |

No analytics targets or conversion benchmarks are set. Any quantitative target needs product agreement.

## 4. Primary flow

1. Open **My comps**: the default MberX Competition, other comps, pending invitations, and search.
2. **Create a comp**: name, code, auto-tip rule, privacy, and Chat, branding and rewards set on or off, with their content. The app generates the private PIN; the captain can reset it in settings.
3. **Invite**: share the unique URL by text or email. The captain sees sent or joined; the invitee sees a pending invitation on My comps.
4. **Join**: tap Accept on My comps (no PIN), or follow the link and enter the six-character alphanumeric PIN, even when signed in. Joining is immediate; no captain approval.
5. **Land**: title, ladder with standing and movement, members and statistics widget, plus branding, Chat and rewards where the captain has enabled them. Captains manage members and settings from settings. Tippers can leave; leaving removes their tips, resets their ladder position and ends reward eligibility.
6. **Tip**: one master card per code and round, shared by every comp. The comp creates no separate tip set. Code and auto-tip rule lock at the first match. Scores reset before the next season.

**Key branches or alternate paths:** A player may have only the default comp. Search may return no matches. A private comp has two join paths: Accept (no PIN) or link (always PIN). Recipients see pending invitations until they accept; captains see sent/joined. Acceptance never waits for approval. Invites, joins, uploads, posts and saves can fail or already be complete. The captain can reset the PIN without invalidating the link; links never expire. How the link creates a pending invitation is To confirm. Code and auto-tip lock at the first match; other settings stay editable. There are no comp-size limits. The landing screen must hold up with empty Chat, or when the player is the only non-captain member.

## 5. Screen inventory

| Order | Screen / view | User goal | Key information and actions | Entry / exit |
|---:|---|---|---|---|
| 1 | My comps | See, search and choose a comp, or accept an invitation | Default comp; joined comps; pending invitations with Accept; in-place search; create and enter | App navigation → comp, create, search, invitation |
| 2 | Create a comp | Configure and create | Name; AFL or NRL; auto-tip rule; public/private; Chat, branding and rewards on or off; reward text per placing and round; logo | My comps → success or recoverable error |
| 3 | Comp landing screen | Take in the whole comp | Title; branding when enabled; ladder with correct tips, margin total, most-recent ordering, own row and movement; members roster; statistics widget; Chat when enabled; rewards when enabled | My comps → settings or tipping |
| 4 | Comp settings | Manage the comp and its members | Setup; **Chat, branding and rewards each enabled or disabled**; logo and reward text (200 words each); PIN reset; **member management: invite by URL, remove tippers**; code and auto-tip read-only after the first match | Landing → save or recoverable error |

The landing screen carries the title, ladder, members and statistics widget, plus branding, Chat and rewards when the captain has enabled them. Settings is the separate management surface and owns member management and the three on/off settings. Chat is not a direct-message feature.

## 6. State coverage

| Screen / component | Relevant state | Expected user need / design response | Notes |
|---|---|---|---|
| My comps | Loading / error | Show structure and a recovery path | Never look like the default comp is missing |
| My comps | Default only / additional comps | Recognise the default comp; find create and join | Card summaries depend on ladder data |
| My comps search | Searching / no matches / failure | Explain no matches; allow a new search | Ordering and filters To confirm |
| Create a comp | Validation / submitting / success / failure | Explain required fields, keep entered values, prevent duplicates | Required fields and success response To confirm |
| Auto-tip rule | Zero points / away team | Make the fallback explicit before creation; show the saved rule | Missing tip resolves at match start or lockout; void, postponed and abandoned fixtures score zero for everyone |
| Brand/logo | Disabled / enabled / upload / invalid / pending / failed | Show branding on the landing screen only when enabled; preview, constraints, recoverable errors | Approval and file rules To confirm |
| Invitation on My comps | Pending / accepting / joined / failure | Distinct from membership; Accept with no PIN; confirm after joining | Links never expire; don't send the player back to the original message |
| Invitation link join | PIN required / invalid / joined / failure | Require the PIN even when signed in; allow re-entry | No attempt limit or lockout |
| PIN in settings | Generated / reset | Show that the app generated it; confirm the reset | Reset invalidates the PIN, not the link |
| Landing — ladder | Loading / no data / populated / movement | Distinguish no data from zero; own row and movement obvious in place | Order: tips, margin total, most recent; movement period To confirm |
| Landing — members | Populated / long roster / no others | Scannable roster; no management controls here | Two members is a realistic early state |
| Landing — statistics widget | Populated / no data / loading | Compact, secondary to the ladder | Content To confirm |
| Landing — Chat | Disabled / empty / populated / posting / failed / image upload / removed post | Show Chat only when enabled; text, image and emoji in place; captain removal clear | Whether disabling hides existing posts To confirm |
| Settings | Before / after first match | Lock code and auto-tip; keep the rest editable | Which settings stay editable To confirm |
| Settings — Chat, branding, rewards | Enabled / disabled | One clear on/off control each, stating what it turns on; disabling takes effect on the landing screen | Defaults, and whether existing content is hidden or kept, To confirm |
| Settings — member management | Invite / sent / joined / removing / removed | Keep invite and remove in settings, apart from the roster; confirm consequences | Leave removes tips, resets position, ends reward eligibility; captain removal changes nothing else |
| Rewards | Disabled / entry / over limit / populated | Show rewards only when enabled; free text per placing and round; captain fulfils outside MberX; stop at 200 words with a count | No catalogue or fulfilment flow |
| Season rollover | Before next season | Show tips and margin resetting to zero one week out | Whether reward eligibility resets To confirm |

## 7. Components and patterns

Use the dark HeroUI direction in `DESIGN.md`. Search the library before custom work and name the candidate checked. No MberX comp-specific component source exists yet.

| Pattern / component | Direction | Source or rationale | Design notes |
|---|---|---|---|
| Buttons, fields, alerts, modals | Reuse | HeroUI candidates; verify in library | One primary action per context; destructive actions must not look like navigation |
| Comp card and search | Adapt | HeroUI `Card` / `Surface`, `Input` | Scannable identity and standing; never imply per-comp tips; mark the default comp |
| Comp landing composition | New | No existing MberX comp screen | Carries title, ladder, members and statistics widget, plus branding, Chat and rewards when enabled; ladder highest. Navigation pattern To confirm |
| Feature on/off setting | Adapt | HeroUI `Switch` / toggle candidate; verify in library | One control each for Chat, branding and rewards, with the consequence stated. Default state To confirm |
| Ladder and member list | Adapt | HeroUI `Table` / list patterns | Must survive a phone; roster is read-only here |
| Statistics widget | New | Compose from HeroUI surfaces | Compact, secondary; content To confirm |
| Settings member management | Adapt | HeroUI `Input`, `Button`, `Modal` / `AlertDialog` | Invite and remove live in settings only |
| Create form | Reuse | HeroUI field and validation patterns | Mark required fields up front; keep values on error |
| Invitation URL share | Adapt | HeroUI `Button` / share actions | Captain sends it; the app does not email or text |
| Pending invitation | Adapt | HeroUI `Card`, `Button` | On My comps, separate from joined comps; Accept needs no PIN |
| Invitation link join | Adapt | HeroUI `Input`, `Button` | PIN required even when signed in |
| PIN reset | Adapt | HeroUI field, `Button` | Reset invalidates the PIN, not the link |
| Branding/logo | Adapt | HeroUI upload / field patterns | Shown only when branding is enabled; rules To confirm |
| Ladder movement | Adapt | HeroUI table/list, semantic status | Text or icon as well as colour |
| Chat composer and posts | Adapt | HeroUI `Input`, `Button`, upload, list | Shown only when Chat is enabled; text, image, emoji; captain remove only |
| Reward entry | Adapt | HeroUI `Input` / `Textarea` | Shown only when rewards are enabled; 200 words per entry; no picker |
| Season reset notice | Adapt | HeroUI semantic status | One week before the season |
| Join / leave confirmation | Adapt | HeroUI `Modal` / `AlertDialog` | Only for consequential actions |
| Empty, success, error feedback | Reuse / Adapt | HeroUI status and alert patterns | Pair colour with labels; offer recovery |

Icons: HeroUI Icons first, Lucide only as fallback. Do not rebuild a component the library already provides.

## 8. Content language and tone

- **Language / locale:** Australian English. Dates as `14 Nov 2026`; times in AEST/AEDT (Sydney).
- **Tone:** Matey, confident, quick-witted. Sports-bar energy, never casino energy.
- **Terminology:** **My comps**, **comp**, **competition**, **player/tipper**, **captain**, **ladder**, **tip**, **fixture**, **round**, **Chat**. Make clear one master card serves every comp.
- **Content constraints:** Sentence case. Full stops in helper text, none in one-sentence buttons. Follow the compliance guardrails in `AGENTS.md`. No betting or wagering language, odds, cash-out language or winning claims.
- **Copy to explore:** Illustrative only: "My comps" and "One set of tips. Every comp you're in gets them." Align final copy to the PIN, reward-text and season-reset rules.

## 9. Design-system requirements

- Follow `AGENTS.md` and `DESIGN.md`; dark theme only.
- Search HeroUI before custom UI; name the candidate and explain any mismatch.
- Use library components and semantic colour, spacing, radius, type and effect tokens. No hardcoded values where a token exists.
- Keep instances linked, use Auto Layout, and name frames and layers semantically.
- Use status colour only for status, always paired with text or another indicator.
- Design mobile first and one-handed; web is a wider view, not a second product.

## 10. Constraints, dependencies, and open questions

- **Constraints / non-negotiables:**
  - Every player is automatically in the global MberX Competition.
  - Players create public or private comps. Search and pending invitations live on My comps.
  - Setup: name, sports code, auto-tip rule, public/private, and Chat, branding and rewards each set on or off. No chat content-filter setting.
  - Invitations: unique URL, sent manually by text or email. Statuses sent, pending, joined. Accept on My comps needs no PIN; the link always does. No captain approval. Links never expire; no PIN attempt limit; reset invalidates the PIN, not the link.
  - The landing screen carries title, ladder, members and statistics widget, plus branding, Chat and rewards when enabled.
  - Settings carries setup, PIN reset, member management (invite and remove), and the on/off controls for Chat, branding and rewards. None of these management controls lives on the landing screen.
  - Chat, branding and rewards are each independently enabled or disabled by the captain. A disabled feature does not appear on the landing screen. The default state of each is not yet decided.
  - Captains manage all comp aspects, remove tippers and remove Chat posts. Tippers can leave.
  - Code and auto-tip rule lock at the first match; other settings stay editable.
  - A missing tip becomes zero points or the away team at match start or lockout, per the comp's rule. Void, postponed and abandoned fixtures score zero for everyone.
  - Removing a tipper changes nothing else. Leaving removes all tips, resets ladder position and ends reward eligibility.
  - Ladder order: correct tips, then lowest margin total (sum of first- and last-round margin picks), then most recent submission.
  - Tips and margin reset to zero one week before the next season.
  - Rewards are captain-entered text, 200 words per entry, fulfilled outside the app and not drawn from the MberX reward programme.
  - Chat: text, image and emoji. No offensive-content hiding, no mute, no related captain setting.
  - No comp-size limits.
  - Tipping is per code, not per comp. One master card serves all comps; never design duplicate per-comp tips.
  - Comp sentiment percentages appear only after the round locks.
  - AFL and NRL only. No extra sports, Flexi, Streak, odds, paid entry, ads or editorial carousel.
  - Do not invent social, membership, permission, discovery or admin behaviour beyond these decisions and `AGENTS.md`.
- **Dependencies:** Agreed score and margin source of truth; logo upload and corporate brand rules.
- **Open questions:**

| Question | Who / what resolves it | What it blocks |
|---|---|---|
| What is the default state of the Chat, branding and rewards settings? | Product | Create form and settings defaults |
| When a feature is disabled, is existing content hidden, kept, or deleted? | Product | Disabled states and any confirmation copy |
| What logo constraints, approval and removal rules apply? | Product / corporate partner | Branding upload and saved states |
| How is captain post removal communicated to the comp? | Product / moderation owner | Chat moderation states and copy |
| Which statistics appear in the landing widget? | Product | Widget content and its states |

- **Assumptions:** Accepting on My comps needs no PIN; following the link always does. Rewards are captain-entered text fulfilled outside MberX. The ESPN audit is a source of interaction ideas only; its unverified behaviour is not a MberX requirement.

## 11. Figma file organisation and handoff

Verify the target file and team conventions before starting.

1. **`00 Index`** — brief, scope boundary, open decisions.
2. **`01 Flows`** — Accept without PIN, link join with PIN, create and invite, public search, landing, settings member management and feature toggles.
3. **`02 Explorations`** — landing hierarchy, the on/off settings and their disabled states, with rationale.
4. **`03 Mobile`** — selected direction, ordered paths, key states.
5. **`04 Web`** — equivalent wider layouts and states.

- **Frame ordering:** Follow the primary flow. Name frames `[flow] / [order] [view] / [state]`, e.g. `COMPS / 01 Overview / Default only`, `CREATE / 02 Details / Validation`, `JOIN / 02 Results / No matches`, `COMP / 03 Landing / Populated`, `COMP / 03 Landing / Chat off`, `COMP / 04 Settings / Feature toggles`, `COMP / 04 Settings / Member management`.
- **Responsive variants:** Mobile-first app view and web view. Use the team's viewport frames; exact dimensions To confirm.
- **Conventions:** Explicit dark theme; HeroUI library-first; MberX naming and atomic design for genuinely shared components.
- **Handoff expectation:** Cover My comps with pending invitations, Accept without a PIN, link join with PIN, the landing screen composed with branding, Chat and rewards both on and off, settings with feature toggles, member management and PIN reset, creation and settings before and after the first match, ladder order and movement, leave consequences, Chat posting and post removal, reward text with its 200-word limit, and the season reset. Annotate open decisions; do not present unresolved rules as settled.

## 12. Review checklist

- [ ] The default MberX Competition is clearly identified.
- [ ] Nothing implies a separate set of tips per comp.
- [ ] My comps shows pending invitations apart from joined comps, with Accept.
- [ ] Accept needs no PIN; following the link always does, even when signed in.
- [ ] PIN reset invalidates the PIN but not the link; links are shown as non-expiring.
- [ ] Creation and invitation states have clear feedback and recovery.
- [ ] The landing screen carries title, ladder, members and statistics widget, plus branding, Chat and rewards when enabled; ladder highest.
- [ ] Chat, branding and rewards each have an on/off setting in settings and creation, and disabled features are absent from the landing screen.
- [ ] Invite and remove live in settings; the landing roster is read-only.
- [ ] Ladder order is correct tips, then lowest margin total, then most recent submission; movement is not colour-only.
- [ ] Leaving is confirmed and states tips removed, position reset, reward eligibility ended; captain removal changes nothing else.
- [ ] Void, postponed and abandoned fixtures show zero for everyone.
- [ ] Mobile and web expose equivalent essential information and actions.
- [ ] Chat supports text, image and emoji, with captain removal and no filter or mute.
- [ ] Rewards are captain text, 200 words, fulfilled outside the app, no picker.
- [ ] The season reset is shown as one week before the new season.
- [ ] No extra sport, custom scoring, paid entry, odds or advertising crept in.
- [ ] HeroUI candidates were checked; deviations are explained.
- [ ] Dark theme, Australian English and MberX terminology are reflected.
- [ ] Open decisions remain visible rather than silently resolved.
