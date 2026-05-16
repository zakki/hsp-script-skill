---
name: hsp-script
description: Write, edit, review, or explain Hot Soup Processor scripts for HSP3/OpenHSP. Use when Codex works on .hsp, .as, or HSP help/example code; creates HSP desktop, HSPCL, HSP3Dish, HGIMG4, module, or sample scripts; ports logic to or from HSP; debugs HSP syntax/runtime behavior; or needs OpenHSP repository conventions for HSP code.
---

# HSP Script

## Workflow

1. Identify the target runtime before writing code: standard HSP3 windowed script, HSPCL console script, HSP3Dish/mobile/web style script, HGIMG4/3D script, module `.as`, or repository test/sample.
2. Inspect nearby `.hsp`, `.as`, or `hsphelp/*.hs` files when working inside an existing project. Prefer established includes, command style, encoding, labels, and asset paths.
3. Write small, direct HSP code. Keep command statements simple, avoid inventing C-like syntax, and preserve HSP idioms such as labels, `gosub`, `goto`, `repeat`/`loop`, `if` command forms, and implicit variable creation where appropriate.
4. If the task touches nontrivial syntax, modules, preprocessing, arrays, strings, HSP3Dish, HGIMG4, external DLL calls, or OpenHSP tests, read `references/hsp-notes.md` before editing.
5. Validate with the most local command available. In this OpenHSP repo, prefer existing test scripts or build tools around the touched area; otherwise at least re-read syntax against nearby examples and mention that runtime verification was not available.

## Code Style

- Use lowercase HSP commands and labels unless matching existing code.
- Use `;` for comments. Keep comments short and practical.
- Put includes and preprocessor directives at the top, for example `#include "hsp3dish.as"` or `#module`.
- Prefer clear ASCII identifiers for new code unless the surrounding script already uses Japanese identifiers.
- Keep one main action per line. Avoid packing unrelated commands into colon-separated one-liners in new code.
- Use explicit initialization for screen, font, color, assets, arrays, and loop counters so generated examples run predictably.
- For HSP3Dish/HGIMG4, include the correct common header and follow sample structure from `sample/hsp3dish`, `sample/hgimg4`, or `common/*.as`.

## Output Expectations

When creating a script from scratch, provide a complete runnable `.hsp` unless the user asks for a fragment. Include required `#include` lines, initialization, the main loop if needed, and a clean `stop` or `end` path.

When reviewing or debugging HSP code, lead with concrete syntax/runtime risks, then give a corrected snippet. Be careful with:

- `repeat`/`loop` nesting and `cnt` scope.
- `if` syntax and multi-command branches.
- Array dimensions and implicit type changes.
- String concatenation, numeric conversion, and system variables.
- Asset paths relative to the script or OpenHSP sample layout.
- Runtime-specific commands that do not exist in HSPCL, HSP3Dish, or HGIMG4.

## Reference

Read `references/hsp-notes.md` for syntax notes, common patterns, and OpenHSP repo-specific locations.
