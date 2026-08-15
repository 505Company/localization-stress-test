---
name: localization-stress-test
description: Stress-test selected Figma screens, components, or flows for localization readiness. Use when a user asks to check translations, internationalization, text expansion, pseudolocalization, RTL, locale-specific dates/numbers/currencies, truncation, wrapping, or whether a design will survive multiple languages. Preserve source designs, create locale-pressure variants on the canvas, identify failures with evidence, and produce a prioritized remediation board. This is a design-readiness audit, not linguistic translation or legal localization review.
---

# Localization Stress Test

Test whether a design system survives the geometry and direction changes caused by localization. Work from evidence on the selected canvas objects. Do not claim that generated sample copy is a validated translation.

## Execute in Figma

1. Inspect the current selection through the Plugin API and identify editable top-level frames, components, or sections.
2. Summarize the selected scope and visible design character in 2–4 sentences. If the selection is usable and the request is unambiguous, continue without asking the user to approve the audit structure.
3. Create the complete audit as a sibling section. Modify only duplicates and clearly labeled proposals.
4. Before editing text, inspect mixed text styles and load every affected font style with `figma.loadFontAsync()`. Preserve style ranges; edit only overrideable text in instances.
5. Create nodes in bounded batches, assign stable names, and retain their IDs for the final response.
6. Re-read the created section and capture a screenshot. Verify label alignment, readable evidence, unclipped text, and separation between source, findings, and proposals.

Finish with clickable links to the audit section, evidence matrix, and proposal row when present. Use node IDs returned by Figma; do not invent links.

## Before editing

1. Identify the selected top-level frames or components and their product context.
2. Determine whether the user supplied target locales, approved translations, content limits, or platform requirements.
3. Use approved translations when available. Otherwise use clearly labeled stress content from [references/pressure-profiles.md](references/pressure-profiles.md).
4. Load the foundational Figma canvas-writing skill before using a Figma canvas write tool.
5. Preserve the source. Never rewrite, detach, resize, or reorganize the selected originals.

If no editable selection is available, ask the user to select one or more frames. If the environment is read-only, return the audit as a structured report without pretending to create canvas objects.

## Choose the test scope

Use the smallest scope that answers the request:

- **Quick scan:** one frame, Long Copy + Format Shift.
- **Interface audit:** selected frames, all applicable profiles.
- **Flow audit:** critical path plus entry, validation, error, empty, and success states.
- **Component audit:** component set, every text-bearing variant, and narrowest supported width.

Apply user-named locales first. When none are named, select profiles by failure mode rather than guessing markets.

Keep profiles in separate variants by default so every failure has an attributable cause. Combine profiles only in an optional final composite after the isolated tests are documented.

## Protect the source

Create a sibling section named `Localization stress test — YYYY-MM-DD`. Put all generated material inside it.

For every source frame:

1. Create a baseline duplicate labeled `00 · Baseline`.
2. Create one duplicate per pressure profile.
3. Keep original component instances connected when duplication permits it.
4. Preserve text styles, variables, effects, constraints, prototype connections, and layout modes unless a test explicitly changes one.
5. Never present a remediation experiment as production-ready design.

## Apply locale pressure

Read [references/pressure-profiles.md](references/pressure-profiles.md) and apply only relevant profiles.

Change content before changing layout. A test is invalid if the agent silently fixes the layout while introducing the stress condition.

For each duplicate:

1. Replace user-visible text with approved translation or labeled stress content.
2. Change dates, numbers, currencies, names, addresses, and units where present.
3. Preserve the original viewport and component dimensions during the first pass.
4. For RTL, mirror reading order and directional UI semantics; do not merely right-align text.
5. Do not mirror universal media controls, non-directional symbols, or brand marks.
6. Record every visible failure before proposing a fix.

When a user names a locale but supplies no approved translation, name the variant after the pressure rather than the language: for example, use `Long Copy — synthetic stress content`, not `German`. Use `RTL geometry test — sample content`, not `Arabic translation`. Ask for approved copy only when linguistic accuracy is required; do not block a geometry audit on it.

## Detect failures

Inspect the entire variant and classify each finding:

- **Blocked:** content is hidden, overlaps an action, becomes unreachable, or reverses meaning.
- **Broken:** truncation, clipping, collision, incorrect ordering, misleading formatting, or unusable control size.
- **Fragile:** survives the sample but has insufficient headroom or depends on accidental spacing.
- **Pass:** survives the tested profile without material degradation.

Check at minimum:

- text clipping, ellipsis, orphaned words, and unexpected line count;
- fixed-height containers and vertically centered text collisions;
- buttons, tabs, chips, segmented controls, tables, and navigation;
- icon-label spacing and directional icon semantics;
- auto-layout wrapping, absolute-positioned text, and nested fixed widths;
- date, time, number, currency, percent, unit, name, and address formats;
- text embedded in images or vector outlines;
- inconsistent or unexposed strings that cannot be localized;
- reading order and start/end alignment in RTL;
- content that remains in the source language inside a stress variant.

## Build the evidence board

Arrange variants in rows by source frame and columns by pressure profile. Add three artifacts without covering the UI:

1. **Finding pins** using stable IDs such as `L10N-01`.
2. **Coverage matrix** with frame × profile status.
3. **Remediation queue** sorted by severity, reach, and recurrence.

Each finding must include:

- ID and severity;
- affected frame/component;
- tested profile and exact stress condition;
- observed failure, not a generic principle;
- likely structural cause;
- smallest durable fix;
- whether the fix belongs in content, component, layout, token, or engineering.

Use [references/evidence-and-remediation.md](references/evidence-and-remediation.md) for the board schema and prioritization rules.

## Propose fixes separately

Do not modify the stress variants when documenting evidence. When the user asks to fix issues, create a separate `Remediation experiments` row.

Prefer durable changes in this order:

1. remove unnecessary copy or clarify content hierarchy;
2. allow wrapping or content-driven sizing;
3. replace fixed width/height with min/max constraints;
4. improve auto-layout behavior and start/end semantics;
5. introduce responsive component variants;
6. use truncation only when loss is intentional and recoverable.

Do not solve localization failures by shrinking text below the product's type scale, reducing hit areas, detaching components, or creating one-off overrides.

## Finish with a decision

Report:

- tested frames and profiles;
- counts for Blocked, Broken, Fragile, and Pass;
- the top three systemic causes;
- fixes that should be made in shared components;
- profiles not tested and why;
- whether the selection is `Not ready`, `Conditionally ready`, or `Ready for linguistic QA`.

Use `Ready for linguistic QA`, never `fully localized`: this skill evaluates design resilience, not translation quality, cultural appropriateness, regulatory compliance, or real assistive-technology behavior.

## Guardrails

- Do not invent target locales when the user provides them.
- Do not describe pseudolocalized copy as translation.
- Do not upload product content or screenshots to third-party translation services without explicit permission.
- Do not overwrite approved translations.
- Do not treat character-count ratios as universal truth; they are pressure tests.
- Do not require every frame to pass every profile when the product explicitly excludes that locale or platform.
