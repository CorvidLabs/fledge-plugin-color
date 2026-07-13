---
module: color
version: 1
status: active
files:
  - bin/color
  - ui/index.html

db_tables: []
depends_on: []
---

# Color

## Purpose

Parse HEX, RGB(A), and HSL(A) colors, render normalized HEX/RGB/HSL/CMYK output with an ANSI swatch, and serve the bundled browser color picker on localhost.

## Public API

| Operation | Behavior |
|-----------|----------|
| color input | Parse short/full HEX, RGB(A), or HSL(A) and display four normalized color models. |
| UI mode | Serve the bundled picker on localhost port 3000 and open it in the default browser. |
| help | Print supported forms and examples without starting a server. |

## Invariants

1. Three-digit HEX expands each nibble before conversion.
2. Output HEX is uppercase and RGB channels are integers.
3. HSL and CMYK percentages are rounded to integers.
4. Pure black maps to CMYK 0%, 0%, 0%, 100% without division by zero.
5. Invalid input exits non-zero and does not start the UI server.
6. UI mode serves only the bundled picker (falling back to the documentation HTML when absent).

## Behavioral Examples

```
Given `#ff8800`
When the color command runs
Then it reports `#FF8800`, `rgb(255, 136, 0)`, `hsl(32, 100%, 50%)`, and `cmyk(0%, 47%, 100%, 0%)`
```

## Error Cases

| Error | When | Behavior |
|-------|------|----------|
| Unsupported color syntax | Parsing returns no RGB value | Print the input-specific error and exit 1. |
| Picker file unavailable | Neither bundled UI nor fallback documentation can be read | Return HTTP 500. |
| Port unavailable | Localhost port 3000 cannot bind | Surface the server error and exit non-zero. |

## Dependencies

- Node.js built-in HTTP, filesystem, path, and child-process modules
- bundled `ui/index.html`
- fledge command packaging

## Change Log

| Version | Date | Changes |
|---------|------|---------|
| 1 | 2026-07-12 | Document existing conversion and picker behavior for SpecSync 5 adoption. |
