# Tipping frame — Figma execution plan

> **Status:** Plan only. Do not execute as part of this task.
> **Source:** `docs/briefs/tipping-brief.md` (Tipping — Design Brief)
> **Target:** [Test — node 12:324](https://www.figma.com/design/j3ET1PZaJSMKrJX2iFbgQb/Test?node-id=12-324&t=P2WanBXrhEDY6xUn-1)

## Assumptions

- Create one top-level mobile screen frame: **`Tipping — open`**.
- Show the **partly tipped** state because the brief provides the explicit progress copy
  “3 of 8 picked” and it demonstrates the core task without creating another screen.
- “Create only one frame” means one top-level screen. Internal auto-layout containers
  may be frames, but no alternate screen, component showcase, detached master, or
  neighbouring state may be placed on the canvas.
- Include fixture-level picked, unpicked, locked and bye treatments inside the one
  screen because the brief requires these to be legible at a glance. Do not create
  separate screens for those treatments.
- Use labelled fixture placeholders where the brief provides no schedule. Do not
  invent a real AFL draw, venue, result, sponsor or statistic. Include “GWS” in one team slot only as the brief’s required sizing test.

## Outcome

Create one dark-theme, mobile-first Tipping frame in the supplied Figma file. It lets
a player switch between AFL and NRL, understand the active round, see that one set of
tips serves every comp, pick between two teams for each fixture, see progress and
submit their tips.

The frame represents **AFL · Round 14 · partly tipped**. It contains eight fixture
rows/cards, with three picks visible. One fixture may show the locked treatment and
one compact row may show a bye. No submitted, confirmation, live, results, sentiment,
failure or empty-round state is created.

## Scope guard

### Include

- AFL/NRL code switch, with AFL selected.
- Round identity and next lockout context.
- “3 of 8 picked” progress.
- The one-line master-card explanation.
- Eight two-way fixture choices grouped by date.
- Three visibly selected tips.
- One locked-fixture treatment using the brief’s copy.
- One compact bye treatment.
- Sticky primary action: “Submit tips”.

### Exclude

- Any second screen or alternate state.
- NRL fixture content; NRL appears only as the unselected code-switch option.
- Confirmation, submitted, live, results, void, drawn-match or sentiment UI.
- Missed-lockout, submit-failed and no-fixtures surfaces.
- Comp picker, comp count, comp list, ladder design or comp management.
- Margin, odds, prices, wagering language, mini games, currency and rewards.
- Notification settings or editorial/news content.

## Phase 1 — prepare the Figma task

1. Load `figma-use` and `figma-generate-design` before any Figma write.
2. Create a Figma session for file key `j3ET1PZaJSMKrJX2iFbgQb`, describing the task as
   a single open-state Tipping frame built from the HeroUI library.
3. Treat node `12:324` as the requested destination context. Inspect its node type and
   page before deciding whether the screen should be placed inside it or beside it.
4. Read the target page structure without mutating it. Record:
   - page name and target-node type;
   - existing top-level frames and their bounds;
   - existing mobile frame width and naming conventions, if any;
   - local variables, styles and components already present.
5. Choose a clear canvas position that does not overlap existing work.

## Phase 2 — discover the HeroUI design library

Run discovery before building. Do not rely on remembered component names or keys.

1. Call `get_libraries` for the target file.
2. Identify the attached HeroUI/MberX library by its returned name and key. Restrict
   all subsequent design-system searches to that library. Use the attached icon
   library only when the HeroUI library has no suitable icon.
3. Run one batched `search_design_system` call for assets required by this frame:
   - **components:** Tipping or sports-picks view, segmented control or tabs,
     primary button, card or surface, chip/status, inline disclosure;
   - **variables:** background, surface, foreground, muted, accent, default,
     border/separator, spacing and radius;
   - **styles:** screen heading, section heading, body, label/caption and surface
     effect.
4. Inspect the strongest whole-view candidate first. Reuse it only if it genuinely
   covers two or more required sections without introducing out-of-scope UI.
5. Inspect component properties for the selected code switch, button and status chip:
   - import the component or component set;
   - inspect variants and text/boolean properties using temporary instances;
   - remove all temporary instances immediately;
   - record the exact component keys and property names for the build call.
6. Inspect the library’s text styles to identify the actual product font family.
   Do not assume Inter.
7. Make and record these reuse decisions before building:
   - **Code switch:** prefer HeroUI segmented control, toggle group or tabs in that
     order; custom-build only if no candidate supports two clear selected states.
   - **Submit action:** use the HeroUI primary button.
   - **Locked status:** use the closest HeroUI chip/status component with a lock icon
     and visible “Locked” text.
   - **Fixture card:** check HeroUI Card/Surface first. Compose the specialised
     two-team selector inside the screen when no exact component exists.
   - **Icons:** HeroUI first; Lucide only for a missing check, lock or disclosure icon.
8. Stop discovery once every component, token and style needed for this screen has a
   selected asset or a documented reason for a custom composition.

## Phase 3 — design specification for the single frame

### Canvas and hierarchy

- Use the mobile width established by existing frames; if none exists, use **390 px**.
- Use dark theme only.
- Use a 4 px spacing rhythm and semantic HeroUI variables rather than raw colours or
  arbitrary spacing.
- Prefer spacing and surface levels over heavy borders or shadows. HeroUI dark mode
  should not gain custom card shadows.

### Content order

1. **Screen header**
   - Heading: `Tipping`.
   - Keep it compact; this is a task screen, not a promotional page.

2. **Code switch**
   - Options: `AFL` and `NRL`.
   - AFL selected.
   - Minimum 44 px target height with a visible selected indicator and focus state.

3. **Round context**
   - `Round 14`.
   - Next lockout information in Sydney time.
   - Progress: `3 of 8 picked` using tabular numbers.
   - Do not imply the whole round locks at once; fixture cards retain their own
     kickoff times.

4. **Scope and rules**
   - `One set of tips. Every comp you're in gets them.`
   - `One point per correct tip. Tips lock at kickoff.`
   - Keep the second line visually secondary; if disclosure is used, show it in its
     collapsed presentation only.

5. **Fixture list**
   - Group fixtures under short date headings.
   - Show eight fixtures total.
   - Use placeholders such as `[Home team]`, `[Away team]`, `[Venue]` and `[Kickoff]`
     where the brief has no real schedule.
   - Use `GWS` in one team position to validate the longest
     supported name without inventing a matchup.
   - Each fixture contains:
     - venue and kickoff metadata;
     - two equal, large team-choice targets;
     - team names that wrap safely rather than truncate ambiguously;
     - a selected treatment that combines fill, check icon and team name;
     - a clear unselected treatment that still looks interactive.
   - Three fixture cards show selected tips, making the progress truthful.
   - One fixture shows `Locked · 7:40 pm` with a lock icon and disabled team choices.
     Keep any previously selected team visible.
   - Add one compact row labelled `Bye this round`; do not present it as an empty or
     broken card.

6. **Sticky submit area**
   - Primary button: `Submit tips`.
   - Full available width and at least 44 px high.
   - Keep it enabled for this partly tipped example, but make the partial progress
     obvious so the player cannot mistake the round for complete.
   - Do not add confirmation copy; that is another state.

## Phase 4 — build in one Figma write call

Use one `use_figma` call for the complete build. This is feasible because the work is
confined to one page and one top-level screen.

1. At the start of the script, resolve the target page and all selected library
   components, variables and styles in parallel.
2. Validate that no top-level frame with the intended exact name already exists.
   If it does, stop with a clear error rather than delete or overwrite unknown work.
3. Create the single top-level frame named `Tipping — open` at the clear position
   found during inspection.
4. Build its hierarchy from top to bottom using auto layout.
5. Use component instances for the selected HeroUI controls. Keep the specialised
   fixture structure inside the screen; do not create component masters elsewhere on
   the page because the deliverable must contain only one frame.
6. Bind fills, strokes, radii, padding and gaps to imported HeroUI variables wherever
   matching tokens exist. Apply imported text styles rather than recreating type.
7. Load every required font before creating or changing text.
8. Use a data array to create all eight fixtures consistently and safely.
9. Turn off any construction placeholder/shimmer before returning.
10. Return the top-level frame ID, every created or mutated node ID, descendant counts,
    frame bounds, instance/component names, styles used and variables bound.

Do not split the build merely to create checkpoints. If the call fails, follow the
`safeToRetryWithoutCanvasRead` result: retry only when explicitly safe; otherwise
inspect the canvas before deciding how to recover.

## Phase 5 — structural validation

Run one read-only validation call against the returned frame ID before taking the
screenshot.

Confirm:

- exactly one new top-level screen frame exists;
- no temporary discovery instances or component masters remain on the page;
- the frame contains eight fixtures and the compact bye row;
- exactly three picks are visibly selected;
- one locked treatment includes icon, text and kickoff time;
- all reusable controls are instances of the selected HeroUI components;
- text uses the discovered product font and imported styles;
- semantic variables are bound for the main fills, borders, spacing and radii;
- no image fill or flattened screenshot represents the interface;
- touch targets are at least 44 px;
- all content stays within the screen bounds and intended scrolling region.

## Phase 6 — screenshot review and one-pass fix

1. Take one full-frame screenshot at sufficient resolution to read fixture labels.
2. Review it once against this checklist:
   - clear order: code → round → rules → fixtures → submit;
   - AFL selection and `3 of 8 picked` are immediately visible;
   - no clipped or overlapping text, including `GWS`;
   - selected, unselected and locked fixture treatments are distinguishable without
     colour alone;
   - the sticky action does not cover the final fixture or bye row;
   - spacing follows a consistent 4 px rhythm;
   - dark surfaces have sufficient separation without unnecessary shadows;
   - primary and muted text meet WCAG 2.2 AA contrast;
   - no placeholder component labels such as “Button” or “Title” remain;
   - all visible copy uses Australian English and sentence case;
   - no odds, prices, betting or wagering language appears.
3. Write a short defect list from that screenshot.
4. Run exactly one targeted `use_figma` fix call addressing the listed defects. Do not
   rebuild the frame and do not add another state.
5. Take one post-fix full-frame screenshot. This is the final visual evidence. Do not
   take another screenshot unless the fix call failed to execute.

## Copy deck

Use these strings verbatim:

| Location | Copy |
|---|---|
| Screen heading | Tipping |
| Code switch | AFL · NRL |
| Round | Round 14 |
| Progress | 3 of 8 picked |
| Scope line | One set of tips. Every comp you're in gets them. |
| Rules line | One point per correct tip. Tips lock at kickoff. |
| Locked fixture | Locked · 7:40 pm |
| Bye row | Bye this round |
| Primary action | Submit tips |

## Accessibility and handoff checks

- Minimum 44 px touch targets for code options, team choices and submit action.
- Visible focus treatment using the HeroUI accent focus token.
- Selected and locked states use icon/text/shape as well as colour.
- Text contrast is at least 4.5:1.
- Team names may wrap without colliding with check or lock icons.
- Motion is not required for this static frame; future implementation must respect
  reduced-motion preferences.
- Annotate that tips lock per fixture at scheduled kickoff and times render in
  AEST/AEDT (Sydney time).

## Definition of done

- One and only one new top-level frame exists: `Tipping — open`.
- It depicts the partly tipped AFL Round 14 state with truthful `3 of 8 picked`
  progress, one locked fixture treatment and one bye row.
- No alternate screen or state has been created.
- HeroUI discovery decisions and any custom-composition reasons are recorded.
- HeroUI components, variables and styles are reused wherever suitable.
- The frame passes structural validation.
- The initial screenshot has been reviewed, one fix pass has been completed and the
  post-fix screenshot passes the visual checklist.

## Planned Figma call sequence

1. `create_session`
2. `get_libraries`
3. `use_figma` — target/page inspection
4. `search_design_system` — batched HeroUI discovery
5. `use_figma` — inspect selected component properties and font; remove temp instances
6. `use_figma` — build the complete frame in one call
7. `use_figma` — structural validation
8. `get_screenshot` — initial visual review
9. `use_figma` — one-pass targeted fix
10. `get_screenshot` — final post-fix evidence

**Expected total: 10 Figma calls**, assuming no tool failure or mandatory recovery
inspection.
