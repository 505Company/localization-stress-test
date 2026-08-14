# Locale pressure profiles

Use these profiles to expose different failure classes. They are test instruments, not substitutes for native-speaker review.

## Profile selection

| Profile | Use it to expose | Apply to |
|---|---|---|
| Long Copy | horizontal and vertical text expansion | buttons, navigation, cards, dialogs, tables |
| Dense Script | line breaks without ordinary spaces and glyph-density changes | headings, labels, narrow columns, chips |
| RTL Flow | direction, order, anchoring, and icon semantics | navigation, forms, steppers, timelines, mixed content |
| Format Shift | locale-sensitive structured values | commerce, finance, analytics, scheduling, profiles |
| Pseudolocalized Coverage | hard-coded, clipped, or missed strings | any complete screen or flow |
| Real Locale | combined real-world pressure | only with supplied or verified translations |

## Long Copy

Increase visible copy length without changing its meaning or hierarchy.

- Use approximately 130% length for paragraphs and ordinary labels.
- Use approximately 160% for short controls where a few extra words cause disproportionate pressure.
- Preserve punctuation and variables such as names or amounts.
- Prefer natural-looking stress prose over repeated characters.
- Do not increase font size as a proxy for translated length.

Flag fixed-width controls that cannot wrap, ambiguous truncation, excessive modal growth, and rows whose actions are displaced.

## Dense Script

Use clearly labeled CJK-like stress content to test denser glyphs and different line-breaking behavior.

- Do not insert spaces simply to force Western wrapping.
- Keep numerals and product names recognizable when useful.
- Test headings, chips, tabs, and table headers at their original dimensions.
- Treat typography rendering problems separately from translation problems.

If authentic content is required, request approved translations rather than fabricating them.

## RTL Flow

Test directionality as a layout transformation.

- Set text direction and alignment appropriately where supported.
- Reverse horizontal reading order, navigation progression, and start/end anchoring.
- Mirror arrows that express back/forward, previous/next, or sequence direction.
- Keep media play icons, checkmarks, clocks, brand marks, and other non-directional symbols unchanged.
- Inspect mixed-direction strings such as phone numbers, email addresses, URLs, codes, and prices.
- Inspect input adornments, validation icons, breadcrumbs, steppers, charts, and carousels.

When validated Arabic or Hebrew copy is unavailable, label the variant `RTL geometry test — sample content` and evaluate geometry only.

## Format Shift

Replace structured content with visibly different but plausible formats:

- dates: numeric, month-name, and different field order;
- time: 12-hour and 24-hour notation;
- numbers: decimal and grouping separator changes;
- currency: symbol before/after, ISO code, and longer values;
- percent and units: spacing and placement changes;
- names: long multi-part names and single-name cases;
- addresses: multi-line and reordered address structures;
- phone numbers: international prefix and grouping;
- plural-sensitive counters: zero, one, few, and many.

Do not assert that one sample represents every locale. The goal is to reveal layout assumptions.

## Pseudolocalized Coverage

Transform every localizable string so omissions remain obvious.

Use a consistent marker such as `［ ... ］` and accented characters while keeping content readable. Expand the result moderately. Preserve interpolation tokens, product names, URLs, and code identifiers.

Flag:

- any user-facing string left unmarked;
- text flattened into vectors or images;
- content that cannot be edited independently;
- hidden or off-canvas text that unexpectedly appears;
- placeholders or validation messages missing from the test.

## Real Locale

Use user-supplied, approved, or otherwise verified translations exactly. Do not rewrite them to make the design fit. Record the failure first; propose structural changes separately.
