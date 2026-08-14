# Evidence board and remediation

## Board layout

Create one section containing:

1. a title and audit metadata;
2. a grid of baseline and pressure variants;
3. a coverage matrix;
4. a prioritized remediation queue;
5. optional remediation experiments.

Keep generated material outside the source selection and preserve enough spacing for reviewers to compare columns without zoom ambiguity.

## Audit metadata

Record:

- audit date;
- source frame/component names;
- viewport or component widths;
- profiles and target locales tested;
- source of translations: approved, supplied, or synthetic stress content;
- exclusions and assumptions.

## Finding pin

Use a compact label near the failure:

`L10N-07 · Broken · Long Copy`

Connect the pin to the affected object when connectors are available. Avoid covering the failure itself.

## Coverage matrix

Use rows for frames/components and columns for profiles. Cells contain one status:

- `Blocked`
- `Broken`
- `Fragile`
- `Pass`
- `Not tested`
- `Not applicable`

Never convert `Not tested` into `Pass`.

## Remediation queue

Use these fields:

| Field | Meaning |
|---|---|
| ID | Stable finding ID |
| Severity | Blocked, Broken, or Fragile |
| Reach | One instance, component family, flow, or product-wide |
| Evidence | Observable failure and tested condition |
| Cause | Content, component, layout, token, or engineering |
| Durable fix | Smallest reusable change |
| Owner | Design, content, engineering, localization, or shared |

Sort first by severity, then by reach, then by recurrence.

## Systemic cause rules

Promote a finding to a systemic cause when any of these are true:

- the same component fails in two or more frames;
- the same layout assumption fails under two or more profiles;
- the problem originates in a shared component or token;
- a missing string or format affects an entire flow;
- fixing a single instance would leave equivalent failures elsewhere.

## Readiness decision

- **Not ready:** any Blocked issue, or repeated Broken issues in a critical flow.
- **Conditionally ready:** no Blocked issues, but Broken or systemic Fragile issues remain.
- **Ready for linguistic QA:** tested profiles pass with only documented, non-critical exceptions and real translations can now be reviewed in context.

This decision applies only to the audited selection and tested profiles.

## Remediation experiment rules

- Duplicate the failing stress variant before changing it.
- Keep stress content unchanged while testing the fix.
- Prefer shared component or token changes when the cause is systemic.
- Show before and after side by side.
- Mark experiments as proposals until reviewed.
- Re-run every profile affected by a shared change.
