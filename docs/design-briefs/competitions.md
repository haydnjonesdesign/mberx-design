# Competitions — UI/UX Design Brief

**Status:** Draft  
**Prepared:** 18 Nov 2026  
**Product / area:** MberX mobile app and web · competitions  
**Design owner / stakeholders:** To confirm

> **Product constraints:** `AGENTS.md`  
> **Inspiration, not a specification:** `docs/ux-audit/espn-footytips/competitions/espn-footytips-competitions-ux-spec.md`. Reuse useful product principles, not ESPN's feature set or visual design.

## 1. Outcome

- **What we are designing:** The MberX experience for seeing/searching comps, creating and managing public or private comps, joining through an invitation or discovery, and the comp landing screen that carries the comp's identity, standings, members, statistics and Chat.
- **Desired user outcome:** A player can get into the right comp, bring their crew together, and see where they stand without leaving the comp to find the ladder, the members or the banter.
- **Why now / product context:** Comps provide the social context for MberX's weekly tipping loop. Every player already belongs to the global MberX Competition; private comps and public/private comp joining extend that experience.
- **Scope:** The comps overview with in-place search; public/private comp creation and joining; the comp landing screen (title, branding, ladder, members, statistics widget, Chat); comp settings including member management (inviting and removing); invitation URLs and sent/joined statuses; corporate branding; ladder and tipper movement; comp Chat with text, image and emoji posts and captain post removal; captain-entered reward text per placing and round; season score reset; responsive mobile and web designs. Show the MberX Competition as the player's default comp.
- **Out of scope:** New sports or game modes; Flexi/Streak or odds-based scoring; paid entries or purchase flows; a reward catalogue, reward selection from the MberX reward programme, or in-app reward fulfilment; direct messages, reactions or chat notifications; back-office tools. These are not established MberX capabilities. Keep the remaining moderation and reward-entry details that are not specified visible as open decisions.

The ESPN audit is useful as evidence that players benefit from an at-a-glance view across comps, a clear creation sequence, and a consistent comp context for standings and membership. Do not copy its per-comp tipping model: MberX has one master tipping card per code and round, shared across every comp. Do not copy ESPN's game modes, fees, ads, sport catalogue, or navigation wholesale.

## 2. Audience and user context

- **Primary audience:** The captain, who creates and manages a comp, invites their crew and wants control and visibility; and the casual tipper, who wants to find their comp and quickly see how they are tracking.
- **Need / situation:** A captain configures a comp, shares an invitation link and manages its settings and Chat. A player may search for and join a public comp, accept a pending private-comp invitation on My comps without a PIN, or join a private comp through its invitation URL using the app-generated six-character alphanumeric PIN, then return to check the ladder. The captain can reset the PIN in settings. Every player also has the default MberX Competition.
- **Current behavior or pain point:** MberX's documented product model includes a default MberX Competition, public/private comps, invites and ladders. Detailed screens and interaction rules for the expanded competition management experience are not specified here. Treat the ESPN UX audit as reference material only, not evidence of MberX behavior.
- **Secondary audiences or roles:** The superfan, who wants useful ladder context without clutter; the reward hunter, who needs any assigned placement reward and winning round to be clear without turning the comp into a shopfront.
- **Accessibility, device, or environment context:** Mobile-first, one-handed use; web is a wider view of the same product. Keep names, standings, membership status and key actions clear at both sizes. Do not claim a formal WCAG conformance level.

## 3. Success criteria

| Criterion | How it will be observed | Source / status |
|---|---|---|
| A player can tell which comps they belong to, including the default MberX Competition | Ask players to identify their comps and the default one from the overview | Product requirement |
| A captain can create a public or private comp and find the next step to bring players in | Observe an unassisted creation-to-invitation prototype task | Product capability; flow details To confirm |
| A player understands that accepting a pending invitation on My comps needs no PIN, while following the invitation link requires it | Ask what action they would take for each comp type and entry point | Product rule |
| A player can see a pending comp invitation on My comps and accept it there | Give a player a pending invitation and ask them to join without opening the original share channel | Product requirement |
| A captain understands the two auto-tip options and when sports code/auto-tip settings lock | Ask them to explain the setting and what they can still change after the first match starts | Product rule |
| Players can explain ladder ranking and identify their movement | Ask players to rank sample tipsters and describe their own movement | Product rule |
| A player can tell which reward is assigned to which placing and round | Ask players to interpret a sample reward schedule | Product capability |
| A player understands that leaving a comp removes their tips and reward eligibility | Ask them to describe what happens if they leave | Product rule |
| A player understands that tips are shared across their comps, not entered separately in each one | Ask what happens to their other comps after tipping | Product requirement |
| A player can find their standing, the member list and Chat on the comp landing screen at both widths | Ask players to locate each section and their own ladder row without leaving the screen | Proposed design check; movement period To confirm |
| A captain can invite and remove members without hunting outside the comp | Ask a captain to invite a player and remove one | Product requirement |

No analytics targets or conversion benchmarks are established. Any future quantitative target needs product agreement.

## 4. Primary flow

1. Open **My comps** and see the default MberX Competition alongside other comps and pending invitations; search for a comp from this screen.
2. Choose **Create a comp**; set its name, applicable code, auto-tip rule, privacy, manually entered placement/round rewards and, for a corporate comp, branding. The app generates the private-comp PIN; the captain can reset it in settings.
3. From the new comp, share its unique invitation URL. The captain can send it manually through text message or email and see whether it is sent or joined; the invitee sees a pending invitation on My comps until accepting.
4. A player can join a public comp from search, or see a pending invitation on **My comps** and tap **Accept**. Accepting a pending invitation in the app needs no PIN. A player following the invitation link must still enter the app-generated six-character alphanumeric PIN, even when already signed in. Successful acceptance joins immediately, with no captain approval step.
5. Land on the comp screen and take in the whole comp in one place: title and branding, the ladder with personal standing and movement, the member list, the statistics widget and Chat. Captains manage members — inviting and removing — from comp settings. Tippers can leave; leaving removes the player's tips, resets their ladder position and ends their reward eligibility.
6. From the comp, go to tipping; tip once on the code's master tipping card. The comp does not create a separate tip set. After tipping has commenced, the captain cannot change the sports code or auto-tip rule. Before the next season starts, comp player scores (tips and margin) reset to zero.

**Key branches or alternate paths:** Players can arrive with only their automatically joined MberX Competition; comp search may return no matches. A private comp can be joined two ways: accepting the pending invitation on My comps, which needs no PIN, or following the invitation link, which always requires the app-generated PIN. Recipients see pending invitations until they accept, while captains can see sent/joined status. Acceptance does not wait for captain approval. An invite, join, upload, post or save may fail or already be complete. The captain can reset the PIN without invalidating the link, and links do not expire. How the link creates or associates a pending invitation remains to confirm. Tipping commences when the first match starts; from then the sports code and auto-tip rule are locked while other settings remain manageable. There are no comp-size limits. The comp landing screen must hold up when Chat is empty or when the player is the only non-captain member.

## 5. Screen inventory

| Order | Screen / view | User goal | Key information and actions | Entry / exit |
|---:|---|---|---|---|
| 1 | My comps | See, search and choose a comp or accept an invitation | Default MberX Competition; joined comps; clearly distinguished pending invitations with an Accept action; in-place comp search; create and enter actions; concise ladder context | App navigation → comp, create, search or invitation acceptance |
| 2 | Create a comp | Configure and create a comp | Name; AFL or NRL code; auto-tip rule (zero points or away-team result); public/private; placement and round rewards entered as free text; optional corporate brand/logo | Overview → create success or recoverable error |
| 3 | Comp landing screen | Take in the whole comp and check standing | **Title and branding** (name, logo, privacy/PIN context); **ladder** with correct-tip count, margin total (sum of the player's first/last-round margin picks), most-recent-tip ordering, the player's row and movement up/down; **members** roster; **statistics widget**; **Chat** with text, image and emoji posts. Route to tipping and, for captains, to settings | Comp selection from My comps → settings or tipping |
| 4 | Comp settings | Manage the comp and its members | Editable comp setup, logo, reward text entries (200 words each); reset the app-generated six-character alphanumeric PIN; **member management: invite players with the invitation URL and remove tippers**; sports code and auto-tip rule become read-only once the first match starts | Comp landing → save or recoverable error; back to comp |

The comp landing screen is a single destination, not a tab set. Title, branding, ladder, members, statistics widget and Chat all live on it, in that hierarchy. Settings is the only separate management surface, and it owns member management (inviting and removing) rather than the landing screen. Chat is a section of the landing screen, not a separate destination and not a general direct-message feature.

## 6. State coverage

| Screen / component | Relevant state | Expected user need / design response | Notes |
|---|---|---|---|
| My comps | Loading / error | Understand that comp data is loading or unavailable and have a clear recovery path | Do not show an empty list as though the default comp is absent; default membership is automatic |
| My comps | Only default comp / additional comps | Recognise the MberX Competition and discover create/join actions; distinguish it from player-created comps | Additional cards and summaries depend on confirmed ladder data |
| My comps search | Searching / no matches / failure | Keep search in the comps overview; explain no matches and allow a new search | Search result ordering/filter options To confirm |
| Create a comp | Validation / submitting / success / failure | Explain required fields, preserve entered values, prevent duplicate creation and confirm next steps | Required-field rules and exact success response To confirm |
| Auto-tip rule | Zero-point rule / away-team rule | Make the selected fallback explicit before creation and show the saved rule in settings | A missing tip is treated as a no-tip (zero points) or the away team when the match begins or lockout is enabled; void, postponed and abandoned fixtures award zero points |
| Brand/logo | No logo / upload / invalid file / pending or failed | Show preview, supported constraints and recoverable errors | Corporate brand approval, file constraints and moderation To confirm |
| Invitation on My comps | Pending / accepting / joined / failure | Make the pending invitation distinct from active comp membership; allow Accept from this screen with no PIN; confirm joining only after acceptance | Invitation links do not expire; do not require the player to return to the message containing the share link |
| Invitation URL join | PIN required / invalid PIN / joined / failure | Require the PIN when following the link, even when signed in; explain the PIN and allow re-entry | No attempt limit or lockout applies |
| Private-comp PIN in settings | Generated / reset | Make clear that the app generated the six-character alphanumeric PIN; let the captain reset it and confirm the reset | Reset invalidates the old PIN but not the invitation link |
| Comp landing — ladder section | Loading / no score data / populated / rank movement | Distinguish unavailable data from zero; make the player's position and movement easy to find without leaving the screen | Order is correct tips, then lowest margin total, then most recent tip timestamp; movement reference period To confirm |
| Comp landing — members section | Populated / long roster / no other members | Show who is in the comp and make the roster scannable in place; management actions stay in settings | Only the acting player plus the captain is a realistic early state |
| Comp landing — statistics widget | Populated / no data / loading | Give a compact read on the comp's round or season without competing with the ladder | Which statistics are shown To confirm |
| Comp landing — Chat section | Empty / populated / posting / failed / image upload / removed post | Support text, image and emoji posts in place on the landing screen; make captain removal clear | |
| Settings | Before / after the first match starts | Clearly lock sports code and auto-tip rule from the first match start; allow other settings to be managed | Which other settings stay editable To confirm |
| Settings — member management | Invite available / sent / joined / removing a tipper / removed | Keep inviting and removing in settings, distinct from the landing roster; confirm the leave consequence before acting | Leaving removes all tips, resets ladder position and ends reward eligibility; removing a tipper changes nothing else |
| Rewards | Placement and award-round entry / over limit | Let the captain type reward details for a placing and round; make clear the captain fulfils rewards outside MberX; stop at the 200-word limit with a clear count | No in-app reward catalogue or fulfilment flow |
| Season rollover | Before next season | Show tips and margin scores reset to zero one week before the new season starts | Whether reward eligibility resets with the scores To confirm |

## 7. Components and patterns

Use MberX's dark HeroUI design direction in `DESIGN.md`. Search the HeroUI library before custom work and record the candidate checked; no MberX competition-specific component source is currently documented.

| Pattern / component | Direction | Existing source or rationale | Design notes |
|---|---|---|---|
| Primary and secondary actions | Reuse | HeroUI `Button` candidate; verify against the library | One clear primary action per context; destructive actions must not look like ordinary navigation |
| Comp overview item and search | Adapt | HeroUI `Card` / `Surface` and `Input` candidates | Make comp identity and standing scannable without implying per-comp tips; keep search on My comps; identify the default comp |
| Comp landing composition | New | No existing MberX comp screen; compose from HeroUI surfaces and sections | One screen carrying title, branding, ladder, members, statistics widget and Chat; use in-page sections rather than a tab set, and keep the ladder highest in the hierarchy |
| Search and filters | Reuse / Adapt | HeroUI `Input`, `Select` candidates | Do not add filters until discovery criteria are confirmed |
| Member list and ladder | Adapt | HeroUI `Table` / list patterns | Preserve the player's identity and standings at narrow widths; don't squeeze a desktop-wide table onto mobile. The roster is read-only on the landing screen |
| Statistics widget | New | No existing MberX pattern; compose from HeroUI surfaces | Compact, secondary to the ladder; content set To confirm |
| Settings member management | Adapt | HeroUI `Input`, `Button` and `Modal` / `AlertDialog` candidates | Inviting and removing live in settings only; the landing roster carries no management controls |
| Create form | Reuse | HeroUI field components and validation patterns | Mark required inputs before submission; preserve entered values after recoverable errors |
| Share invitation link | Adapt | HeroUI `Button` / share-action candidates | A unique URL for a private comp requires PIN entry when followed; the captain sends it manually through text or email and sees sent/joined status. Do not imply MberX sends an email or text itself |
| Pending invitation | Adapt | HeroUI `Card` / `Surface` and `Button` candidates | Present on My comps, separate from joined comps, with a clear Accept action; accepting here needs no PIN |
| Invitation URL join | Adapt | HeroUI `Input` and `Button` candidates | Following the link requires the app-generated six-character alphanumeric PIN, even when signed in |
| Private-comp PIN reset | Adapt | HeroUI field and `Button` candidates | Captain can reset the app-generated PIN in settings; reset invalidates the PIN but not the invitation link |
| Comp branding/logo | Adapt | HeroUI upload / field patterns; verify library candidate | Corporate comp branding is supported; exact upload and approval rules To confirm |
| Ladder movement | Adapt | HeroUI table/list and semantic status candidates | Show up/down movement with text or icon as well as colour; keep tip score, margin total and most-recent-timestamp ordering understandable |
| Chat composer and posts | Adapt | HeroUI `Input`, `Button`, upload and list candidates | Text, image and emoji posts; captain-only remove action |
| Reward entry | Adapt | HeroUI `Input` / `Textarea` and form patterns | Captain types reward text per placing and round, up to 200 words per entry; no catalogue picker or fulfilment flow |
| Season rollover notice | Adapt | HeroUI semantic status pattern | Make clear tips and margin scores reset to zero one week before the new season |
| Join / leave confirmation | Adapt | HeroUI `Modal` / `AlertDialog` candidates | Use only for consequential actions; do not turn ordinary navigation into a dialog |
| Empty, success and error feedback | Reuse / Adapt | HeroUI semantic status and alert patterns | Pair colour with labels; provide a recovery action where applicable |

Icons: HeroUI Icons first; use Lucide only if HeroUI has no suitable icon. Do not create a custom component that duplicates a suitable library component.

## 8. Content language and tone

- **Language / locale:** Australian English. Dates use `14 Nov 2026`; times use AEST/AEDT (Sydney time) where relevant.
- **Tone:** Matey, confident and quick-witted; sports-bar energy, never casino energy.
- **Terminology:** Use **My comps**, **comp**, **competition**, **player/tipper**, **captain**, **ladder**, **tip**, **fixture**, **round** and **Chat** accurately. Make clear that one master tipping card serves every comp.
- **Content constraints:** Sentence case. Full stops in helper text; none in one-sentence buttons. Keep compliance guardrails in `AGENTS.md` in view. Never use betting or wagering language, odds, cash-out language, or claims about winning.
- **Copy to explore:** Illustrative only: “My comps” and “One set of tips. Every comp you're in gets them.” Keep final copy aligned to the PIN, reward-text and season-reset rules.

## 9. Design-system requirements

- Follow the MberX design principles in `AGENTS.md` and `DESIGN.md`; use dark theme only.
- Search HeroUI before creating custom UI; identify the matching library candidate and explain any mismatch.
- Use library components and semantic colour, spacing, radius, typography and effect tokens; do not hardcode values where a suitable token exists.
- Keep linked component instances, use Auto Layout throughout, and name frames and important layers semantically.
- Use status colour only for status and pair it with text or another clear indicator. Do not rely on colour alone.
- Design mobile first and one-handed; web is a wider view of the same product, not a separate product.

## 10. Constraints, dependencies, and open questions

- **Constraints / non-negotiables:**
  - Every player is automatically in the global MberX Competition.
  - Players can create public or private comps. Comp search and a player's pending invitations are shown on the My comps screen.
  - Comp setup includes name, applicable sports code, auto-tip rule (zero points or away-team result when a player does not tip), rewards entered as free text by the captain for a placing (winner, second, third or wooden spoon) and round, optional corporate branding and public/private visibility. There is no chat content-filter setting; Chat allows text, image and emoji posts.
  - Invitations use a unique URL for the comp, which the captain sends manually via text message or email. Invitation statuses include sent, pending and joined. A recipient can see a pending invitation on My comps and tap Accept without a PIN. There is no captain approval; accepting joins immediately. A player following the invitation link must still enter the app-generated six-character alphanumeric PIN, even when signed in. Invitation links do not expire. The captain can reset the PIN in settings; resetting it does not invalidate the link. No PIN attempt limit or lockout applies.
  - The comp landing screen carries the comp title, branding, ladder, members, a statistics widget and Chat. It is one destination; Chat and the roster are sections of it, not separate screens.
  - Comp settings carries the comp's setup, rewards, PIN reset and member management: inviting players with the invitation URL and removing tippers. Inviting and removing are not on the landing screen.
  - Captains can manage all comp aspects, remove tippers and remove Chat posts. Tippers can leave. Once tipping has commenced — the moment the first match starts — sports code and auto-tip rule cannot be changed; other settings remain manageable.
  - A missing tip is treated as a no-tip (zero points) or the away team when the match begins or lockout is enabled, per the comp's auto-tip rule. Void, postponed and abandoned fixtures award zero points to everyone.
  - Removing a tipper changes nothing beyond removal: their tips, ladder position and reward eligibility are left as they were.
  - Ladder order is correct-tip count, then the lowest margin total (the sum of the player's first- and last-round margin picks), then the most recent tip submission first.
  - Leaving a comp removes all of that player's tips, resets their ladder position and ends their reward eligibility.
  - Player scores (tips and margin) reset to zero one week before the next season starts.
  - Rewards are not drawn from the MberX reward programme. The captain types reward text in comp settings, limited to 200 words per entry, and fulfils the reward outside the app.
  - There are no comp-size limits.
  - Corporate captains can brand a comp with a logo. Chat supports text, image and emoji posts; there is no offensive-content hiding and no related captain setting.
  - Tipping is per sports code, not per comp. A single master tipping card serves all comps; do not design duplicate per-comp tips or imply comp-specific tipping.
  - Comp sentiment percentages appear only after the round locks.
  - AFL and NRL only. Do not include ESPN's extra sports, Flexi, Streak, betting odds, paid entry, ads or editorial carousel.
  - Do not invent social, membership, permission, discovery or admin behavior beyond the decisions recorded here and in `AGENTS.md`.
  - Use dark MberX styling, Australian English, and mobile-first layouts.
- **Dependencies:** Agreed score and margin source of truth; logo upload and corporate brand rules.
- **Open questions:**

| Question | Who / what resolves it | What it blocks |
|---|---|---|
| What logo file constraints, brand approval and removal rules apply? | Product / corporate partner | Branding upload and saved states |
| How is captain post removal communicated to the comp? | Product / moderation owner | Chat moderation states and copy |
| Which statistics appear in the comp landing widget? | Product | Widget content and its states |

Resolved in this revision, for reference: void, postponed and abandoned fixtures award zero points to everyone; a player following the invitation link must still enter the PIN; resetting the PIN does not invalidate the link; there is no PIN attempt limit; tipping commences when the first match starts; removing a tipper changes nothing else; reward text is limited to 200 words per entry; scores reset one week before the next season starts.

- **Assumptions:** Treat in-app acceptance of a pending invitation on My comps as needing no PIN, and the app-generated six-character alphanumeric PIN as required when following the invitation link. Treat rewards as captain-entered text with fulfilment outside MberX. ESPN's audit is a source of interaction ideas and observed competitor behavior only; its unverified behavior is not a MberX requirement.

## 11. Figma file organisation and handoff

Recommended structure; verify the target Figma file and existing team conventions before starting.

1. **Page: `00 Index`** — brief, scope boundary and key open decisions.
2. **Page: `01 Flows`** — My comps invitation acceptance (no PIN), invitation-URL join with PIN, comp creation/invite, public search, comp landing and settings/member-management flow maps.
3. **Page: `02 Explorations`** — alternatives for the comp landing hierarchy (title, branding, ladder, members, statistics widget, Chat) and for settings member management, with rationale.
4. **Page: `03 Mobile`** — selected direction, ordered primary paths, and key states.
5. **Page: `04 Web`** — equivalent wider layouts and states.

- **Frame ordering:** Match the primary flow. Name frames `[flow] / [order] [view] / [state]`, for example `COMPS / 01 Overview / Default only`, `CREATE / 02 Details / Validation`, `JOIN / 02 Results / No matches`, `COMP / 03 Landing / Populated`, `COMP / 04 Settings / Member management`.
- **Responsive/platform variants:** Mobile-first app view and web view. Use the team's established viewport frames; exact dimensions To confirm.
- **Existing conventions to follow:** Explicit dark theme; HeroUI library-first; MberX naming and atomic-design conventions for any genuinely reusable shared components.
- **Review / handoff expectation:** Show My comps with joined comps and pending invitations, in-app acceptance without a PIN, link-following join with mandatory PIN entry, the comp landing screen as one composed view (title, branding, ladder, members, statistics widget, Chat), settings with member management (inviting and removing) and the generated PIN/reset, comp creation and settings before/after the first match starts, public/private join paths, ladder ordering and movement, leave consequences, Chat posting and captain post removal, reward text entry with its 200-word limit, the season reset, and relevant states. Annotate remaining open decisions; do not present unresolved rules as settled.

## 12. Review checklist

- [ ] The MberX Competition is clearly identified as the default comp.
- [ ] The comp overview does not imply a separate set of tips per comp.
- [ ] My comps shows pending invitations separately from joined comps and lets the player tap Accept there.
- [ ] Public comp search is on My comps; accepting a pending invitation there needs no PIN and joins immediately without approval.
- [ ] Following a private comp's invitation link requires the app-generated six-character alphanumeric PIN, even when signed in.
- [ ] Private-comp settings show that the app generated the PIN and let the captain reset it; reset invalidates the PIN but not the link.
- [ ] Creation and invitation states have clear feedback and recovery; invitation links are shown as non-expiring, with no PIN attempt limit.
- [ ] The comp landing screen carries title, branding, ladder, members, statistics widget and Chat as one destination, with the ladder highest in the hierarchy.
- [ ] Inviting and removing members live in comp settings; the landing roster is read-only.
- [ ] Ladder order is correct tips, then lowest margin total, then most recent tip timestamp; movement is shown without relying on colour.
- [ ] Leaving a comp is confirmed and states that tips are removed, ladder position resets and reward eligibility ends; removing a tipper is shown as changing nothing else.
- [ ] Void, postponed and abandoned fixtures are shown as scoring zero for everyone.
- [ ] Mobile and web expose equivalent essential comp information and actions.
- [ ] Captain/member actions include settings management, post removal, tipper removal and player leave; sports code and auto-tip rule lock from the first match start.
- [ ] Chat supports text, image and emoji posts; captains can remove posts; no offensive-content filter or related captain setting appears.
- [ ] Rewards are captain-entered text per placing and round, limited to 200 words, with fulfilment outside the app and no catalogue picker.
- [ ] The season reset of tips and margin scores to zero is represented as happening one week before the new season.
- [ ] No extra sport, custom scoring, paid entry, odds or advertising surface has been added by implication.
- [ ] HeroUI candidates were checked before custom patterns; deviations are explained.
- [ ] Dark theme, Australian English and MberX terminology are reflected.
- [ ] Open decisions remain visible in the handoff rather than being silently resolved in the mock-up.
