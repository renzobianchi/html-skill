---
name: html
description: Build standalone interactive HTML artifacts as the medium for agent↔designer conversation — review docs with approve/deny/discuss, N-way prototype variants, before/after motion comparisons, visual explorers for APIs/content, and inline-editable copy ecosystems. Use when the user invokes /html or asks for an HTML artifact, review doc, variant board, or visual playground.
---

# HTML artifacts

You produce a **single, standalone `.html` file** that is the closest possible representation of the real thing, plus an interaction layer that turns the user's reactions back into a prompt for the agent. The artifact is not a deliverable — it is one turn in a conversation. Its job is to let the user *see and feel* options instead of imagining them from bullet points, and to make responding as cheap as clicking.

## Non-negotiables

- **One file, zero build.** Inline all CSS and JS. No frameworks, no CDNs unless the fidelity genuinely requires one (e.g. a font); it must open from `file://` and still work.
- **Closest possible representation.** Render the real component, the real animation, the real copy — with the project's actual tokens, fonts, and colors when the artifact is about an existing product. Read the project's CSS/theme first and reuse it. A gray-box approximation defeats the purpose: decisions made on it don't transfer.
- **Always close the loop.** Every artifact that asks for decisions ends with a fixed **"Copy response"** button that serializes the user's selections/edits/notes into a compact, paste-ready prompt (plain text, no JSON dumps) addressed to the agent: what was approved, what was denied, what has notes, verbatim edits. The user pastes *that* back — never the whole doc.
- **Real motion, not screenshots of motion.** If the subject moves, the artifact animates. Add replay buttons; loop only what loops in the product.
- **Cheap to regenerate.** Don't gold-plate the chrome of the artifact itself; spend fidelity on the subject under review. The user may ask for "four more" in the next message.
- Save to a sensible path (project `./artifacts/` or `/tmp` if no project) and tell the user the path; open it with `open <file>` on macOS when a browser exists.

## Pick the format from the user's need

Adapt these — they are shapes, not templates. Combine them when the request spans two.

### 1. Review / decision doc
For audits, proposed changes, refactors, redesign proposals — anything with a list of items the user must judge.
- One card per proposal: title, why, evidence (before/after rendering or code snippet — rendered beats code), severity/tag if relevant.
- Per-card controls: **Approve / Deny / Discuss**, and a free-text note field that appears on Discuss (and is available on all).
- A sticky header or footer with running count (e.g. "8 approved · 3 denied · 2 discussing") and the **Copy response** button.
- If the source review already exists (e.g. a critique file), transcribe it faithfully; don't invent items.

### 2. Variant board
For "show me this N ways" — components, layouts, effects, type treatments.
- Default to 4 variants (6 for micro-effects), each a live rendering at realistic size with a short label naming the *idea* behind it, not "Variant 2".
- Number them so the user can dictate over it: "me gusta la 2 pero…".
- If the variants animate, give each its own replay control.
- If the project has design system documentation (guidelines, token docs, component specs), feed it as the generation instructions: variants explore divergent ideas *inside* the system's constraints, not just skinned with its tokens.

### 3. Motion before/after
For animation changes: current version and proposed version side by side, both live.
- Replay-both button; per-side replay.
- When fine-tuning is the point, add sliders for the real parameters (duration, stiffness/damping or bezier points, distance, blur) that manipulate the live element, and print the current values as copyable code.
- A shared scrubber over a normalized timeline is welcome when comparing easing.

### 4. Visual explorer
For understanding a domain — an API, a dataset, a codebase area.
- Break it into scannable categories; render what each capability could *become* (a card, a chart, a badge) rather than describing it.
- Optimize for scroll-and-react: the user reads it while dictating what interests them.

### 5. Repackaged reading
For content the user wants to consume in a better shape: generous space, slide-sized bites, one idea per screenful. Keep the source's words; change only the container.

### 6. Copy ecosystem
Every system string of a kind (toasts, dialogs, errors, empty states) in one doc, rendered inside a faithful mock of its real component.
- Inline-editable text (`contenteditable`), visually marking edited items.
- Copy response outputs only the changed strings as before → after pairs.

## Craft floor for the artifact itself

- The chrome (headers, buttons, counts) is quiet and neutral; the subject carries the visual weight.
- **Comparison grids compare, so they align.** When variants sit in a grid, every stage is the same size (`grid-auto-rows: 1fr` + each variant a flex column with the stage on `flex: 1`), subjects centered both axes, and the per-variant controls land on one horizontal line. Misaligned Favorite buttons read as sloppiness and bias the comparison toward the tallest card.
- Visual baseline, in one pass: one neutral palette + one accent (semantic colors only for semantics); hierarchy from size and weight, not from more colors; spacing on a 4/8px rhythm with generous padding — when in doubt, more whitespace; either a border or a shadow per surface, rarely both; one border-radius scale (outer > inner); body text ≥ 13px, muted text still ≥ 4.5:1 contrast.
- Interactive things look interactive: hover feedback on anything clickable, visible focus, `cursor: pointer`, transitions 120–200ms ease-out. Nothing else moves unless motion is the subject.
- Interactions need no instructions — if a control isn't self-evident, label it.
- State survives a scroll but need not survive a reload; this is a disposable document. Say so in the footer if the user might assume otherwise.
- Copy button must actually work from `file://`: use `navigator.clipboard` with a `document.execCommand('copy')` fallback, and confirm visually ("Copied ✓").
- Respect `prefers-reduced-motion` in the chrome; the subject's animations still play on demand (replay buttons) since reviewing them is the task.
- Dark/light: match the product under review; if none, follow `prefers-color-scheme`.

## Process

1. Ask nothing if the request names the subject and the format is inferable; otherwise ask one question, not a questionnaire.
2. Gather the real material first (tokens, components, copy, findings). The artifact is only as useful as the truth it renders.
3. Build the full file in one pass. Open it. One batched self-check (does it render, do the controls work, does Copy response produce a sane prompt) — then stop polishing and hand it over.
4. When the user pastes the response prompt back, act on it in the project, not in the artifact; regenerate the artifact only if they ask for another round.

---

*Inspired by the artifact-driven design workflows of [Kyle Zantos](https://x.com/kylezantos) and [Michael Riddering (Ridd)](https://x.com/Ridd_design).*
