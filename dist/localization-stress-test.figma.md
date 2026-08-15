---
name: localization-stress-test
description: Stress-test selected Figma screens, components, or flows for localization readiness. Use for translation expansion, pseudolocalization, RTL, locale-specific formats, truncation, wrapping, or design resilience across languages. Preserve source designs, create locale-pressure variants, identify failures with evidence, and produce a prioritized remediation board. This is a design-readiness audit, not linguistic translation or legal localization review.
---

# Localization Stress Test

Test whether selected designs survive geometry, formatting, and direction changes caused by localization. Work from evidence on the canvas. Never claim that generated sample copy is a validated translation.

## Execute in Figma

1. Inspect the current selection through the Plugin API and identify editable top-level frames, components, or sections.
2. Summarize the selected scope and visible design character in 2–4 sentences. If the selection is usable and the request is unambiguous, continue without asking the user to approve the audit structure.
3. Create the complete audit as a sibling section. Modify only duplicates and clearly labeled proposals.
4. Before editing text, inspect mixed text styles and load every affected font style with `figma.loadFontAsync()`. Preserve style ranges; edit only overrideable text in instances.
5. Create nodes in bounded batches, assign stable names, and retain their IDs for the final response.
6. Re-read the created section and capture a screenshot. Verify label alignment, readable evidence, unclipped text, and separation between source, findings, and proposals.

Finish with clickable links to the audit section, evidence matrix, and proposal row when present. Use node IDs returned by Figma; do not invent links.

## Prepare

1. Identify selected top-level frames or components and their product context.
2. Determine whether the user supplied target locales, approved translations, content limits, or platform requirements.
3. Preserve the source. Never rewrite, detach, resize, or reorganize the selected originals.
4. If no editable selection is available, ask the user to select frames. In read-only environments, return a structured audit without claiming to create canvas objects.

Choose the smallest useful scope:

- **Quick scan:** one frame, Long Copy and Format Shift.
- **Interface audit:** selected frames and all applicable profiles.
- **Flow audit:** critical path plus entry, validation, error, empty, and success states.
- **Component audit:** component set, every text-bearing variant, and narrowest supported width.

## Protect the source

Create a sibling section named `Localization stress test — YYYY-MM-DD`. For every source frame:

1. Create `00 · Baseline`.
2. Create one duplicate per pressure profile.
3. Keep component instances connected when duplication permits it.
4. Preserve styles, variables, effects, constraints, connections, and layout modes unless a test explicitly changes one.
5. Never present a remediation experiment as production-ready design.

## Pressure profiles

Keep profiles separate so every failure has an attributable cause. Combine them only in an optional final composite after isolated tests are documented.

### Long Copy

Increase visible copy length without changing meaning or hierarchy. Use about 130% length for paragraphs and ordinary labels and about 160% for short controls. Preserve punctuation and variables. Do not change font size. Flag controls that cannot wrap, ambiguous truncation, excessive modal growth, and displaced actions.

### Dense Script

Use clearly labeled CJK-like stress content to test dense glyphs and line breaking without ordinary spaces. Test headings, labels, narrow columns, chips, tabs, and table headers at original dimensions. Request approved translations when linguistic authenticity is required.

### RTL Flow

Treat RTL as a layout transformation. Set appropriate direction and alignment, reverse horizontal reading order and start/end anchoring, and mirror arrows that express sequence. Do not mirror media controls, checkmarks, clocks, brand marks, or non-directional symbols. Inspect mixed-direction phone numbers, emails, URLs, codes, and prices. Without validated Arabic or Hebrew copy, label the variant `RTL geometry test — sample content` and evaluate geometry only.

### Format Shift

Use visibly different plausible formats for dates, time, numbers, currencies, percentages, units, names, addresses, phone numbers, and plural-sensitive counters. Do not claim one sample represents every locale.

### Pseudolocalized Coverage

Transform every localizable string with a consistent marker such as `［ ... ］`, accented characters, and moderate expansion. Preserve interpolation tokens, product names, URLs, and code identifiers. Flag unmarked user-facing strings, outlined or image-based text, hidden strings, placeholders, and missing validation messages.

### Real Locale

Use supplied, approved, or verified translations exactly. Never rewrite them to make the design fit. Record failures before proposing structural changes.

When a locale is named but approved translations are absent, name variants after the pressure, not the language. Use `Long Copy — synthetic stress content`, not `German`, and `RTL geometry test — sample content`, not `Arabic translation`.

## Apply pressure

Change content before changing layout. A test is invalid if the layout is silently fixed while stress is introduced.

For each duplicate:

1. Replace visible text with approved translation or labeled stress content.
2. Change relevant dates, numbers, currencies, names, addresses, and units.
3. Preserve the original viewport and component dimensions during the first pass.
4. For RTL, mirror reading order and directional semantics rather than merely right-aligning text.
5. Record every visible failure before proposing a fix.

## Detect failures

Classify every finding:

- **Blocked:** content is hidden, overlaps an action, becomes unreachable, or reverses meaning.
- **Broken:** truncation, clipping, collision, incorrect ordering, misleading formatting, or unusable control size.
- **Fragile:** the sample survives but lacks headroom or depends on accidental spacing.
- **Pass:** no material degradation under the tested profile.

Check text clipping, ellipsis, orphaned words, fixed-height collisions, buttons, tabs, chips, tables, navigation, icon semantics, auto-layout wrapping, fixed widths, locale formats, outlined text, unexposed strings, RTL reading order, and source-language content left inside stress variants.

## Build the evidence board

Arrange variants in rows by source frame and columns by profile. Keep annotations outside the UI. Add:

1. Finding pins using stable IDs such as `L10N-01`.
2. A coverage matrix with frame-by-profile status.
3. A remediation queue sorted by severity, reach, and recurrence.

Each finding includes ID, severity, affected frame or component, tested condition, observed failure, likely structural cause, smallest durable fix, and responsible domain: content, component, layout, token, or engineering.

Coverage cells use only `Blocked`, `Broken`, `Fragile`, `Pass`, `Not tested`, or `Not applicable`. Never convert `Not tested` into `Pass`.

Prioritize remediation first by severity, then reach, then recurrence. Promote a finding to a systemic cause when it affects a shared component, repeats across frames or profiles, affects an entire flow, or would remain elsewhere after an instance-only fix.

## Propose fixes separately

When asked to fix issues, create a separate `Remediation experiments` row and keep stress content unchanged. Prefer:

1. clearer content hierarchy;
2. wrapping or content-driven sizing;
3. min/max constraints instead of fixed dimensions;
4. resilient auto layout and start/end semantics;
5. responsive component variants;
6. truncation only when information loss is intentional and recoverable.

Do not shrink text below the product type scale, reduce hit areas, detach components, or create one-off overrides. Show before and after side by side and re-run profiles affected by shared changes.

## Finish with a decision

Report tested frames and profiles, counts for each status, top systemic causes, shared-component fixes, untested profiles and reasons, and one scoped decision:

- **Not ready:** any Blocked issue or repeated Broken issues in a critical flow.
- **Conditionally ready:** no Blocked issues, but Broken or systemic Fragile issues remain.
- **Ready for linguistic QA:** tested profiles pass with only documented non-critical exceptions.

Use `Ready for linguistic QA`, never `fully localized`. This skill evaluates design resilience, not translation quality, cultural appropriateness, regulatory compliance, or real assistive-technology behavior.

## Guardrails

- Do not invent target locales when the user supplies them.
- Do not describe pseudolocalized or synthetic copy as translation.
- Do not upload product content or screenshots to third-party translation services without permission.
- Do not overwrite approved translations.
- Do not treat character-count ratios as universal truth.
- Do not require excluded locales or platforms to pass.
