---
name: hsp-script
description: Write, edit, review, or explain Hot Soup Processor scripts for HSP3/OpenHSP. Use when Codex works on .hsp, .as, or HSP help/example code; creates HSP desktop, HSPCL, HSP3Dish, HGIMG4, module, or sample scripts; ports logic to or from HSP; debugs HSP syntax/runtime behavior; or needs Windows HSP package or OpenHSP repository conventions for HSP code.
---

# HSP Script

## Workflow

1. Default to the official Windows HSP 3.7 package layout unless the user says they are working in Linux/OpenHSP source. Treat Windows users, HSP Script Editor (`hsed3.exe`), package-root `common/`, `sample/`, `doclib/`, `hsphelp/`, DLL plugins, and `runtime/*.hrt` as the normal target.
2. Identify the target runtime before writing code: standard HSP3 windowed script, HSPCL console script, HSP3Dish/mobile/web style script, HGIMG4/3D script, module `.as`, or package/repository sample.
3. Inspect nearby `.hsp`, `.as`, or `hsphelp/*.hs` files when working inside an existing project. Prefer established includes, command style, encoding, labels, and asset paths.
4. Write small, direct HSP code. Keep command statements simple, avoid inventing C-like syntax, and preserve HSP idioms such as labels, `gosub`, `goto`, `repeat`/`loop`, `if` command forms, and implicit variable creation where appropriate.
5. If the task touches nontrivial syntax, modules, preprocessing, arrays, strings, HSP3Dish, HGIMG4, external DLL calls, package layout, or OpenHSP tests, read `references/hsp-notes.md` before editing.
6. Validate with the most local command available. For normal Windows usage, expect HSP Script Editor or package tools such as `hspcmp.exe`/runtime executables; for Linux+OpenHSP source work, use existing tests or build tools around the touched area. If runtime verification is not available, say so.

## Code Style

- Use lowercase HSP commands and labels unless matching existing code.
- Prefer `;` for comments in new HSP code unless nearby code uses another style. HSP also accepts `//` line comments and `/* ... */` block comments.
- Put includes and preprocessor directives at the top, for example `#include "hsp3dish.as"` or `#module`.
- Prefer clear ASCII identifiers for new code unless the surrounding script already uses Japanese identifiers.
- Keep one main action per line. Avoid packing unrelated commands into colon-separated one-liners in new code.
- Use explicit initialization for screen, font, color, assets, arrays, and loop counters so generated examples run predictably.
- For HSP3Dish/HGIMG4, include the correct common header and follow sample structure from package-root `sample/hsp3dish`, `sample/hgimg4`, or `common/*.as`.

## Output Expectations

When creating a script from scratch, provide a complete runnable `.hsp` unless the user asks for a fragment. Include required `#include` lines, initialization, the main loop if needed, and a clean `stop` or `end` path.

When reviewing or debugging HSP code, lead with concrete syntax/runtime risks, then give a corrected snippet. Be careful with:

- `repeat`/`loop` nesting and `cnt` scope.
- `if` syntax and multi-command branches.
- Array dimensions and implicit type changes.
- String concatenation, numeric conversion, and system variables.
- Asset paths relative to the script, Windows HSP package layout, or OpenHSP sample layout.
- Runtime-specific commands that do not exist in HSPCL, HSP3Dish, or HGIMG4.

## Reference

Read `references/hsp-notes.md` for syntax notes, common patterns, Windows HSP package layout, and Linux+OpenHSP source-tree notes.
