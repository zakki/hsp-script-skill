# HSP Notes

## Runtime Selection

- Standard HSP3: windowed desktop scripts using commands such as `screen`, `mes`, `button`, `color`, `pos`, `line`, and `stick`.
- HSPCL: console or command-line scripts; avoid GUI-only assumptions.
- HSP3Dish: portable/mobile/web-oriented scripts; start from examples under `sample/hsp3dish` and include `hsp3dish.as` when needed.
- HGIMG4: 3D/game scripts; start from examples under `sample/hgimg4` and include `hgimg4.as`.
- Module files: `.as` files commonly define reusable commands/functions with `#module`, `#deffunc`, `#defcfunc`, `#global`, and related preprocessor features.

## Syntax Reminders

- Comments may use `;`, `//`, or `/* ... */`. Prefer `;` in new code unless nearby code uses another style.
- Labels start with `*`, for example `*main`.
- Assignment is commonly `name = value`. Commands are usually command-first, for example `mes "text"`.
- `repeat n` starts a loop and `loop` ends it. `cnt` is the current repeat counter for the innermost loop.
- `if condition : command` is common for short branches. For longer branches, follow existing project style and keep branch bodies easy to scan.
- `goto *label` jumps; `gosub *label` calls a subroutine that returns with `return`.
- Use `stop` to stop a GUI script without closing immediately; use `end` when the program should terminate.
- Preprocessor lines begin with `#`, such as `#include`, `#const`, `#define`, `#module`, `#deffunc`, and `#defcfunc`.

## Common Patterns

Minimal GUI script:

```hsp
screen 0, 640, 480
title "HSP sample"
font "Arial", 24
pos 40, 40
mes "Hello, HSP!"
stop
```

Simple animation loop:

```hsp
screen 0, 640, 480
x = 0

*main
redraw 0
color 255, 255, 255
boxf
color 0, 0, 0
pos x, 200
mes "moving"
redraw 1

x = (x + 4) \ 640
await 16
goto *main
```

Subroutine pattern:

```hsp
gosub *init
mes message
stop

*init
message = "ready"
return
```

Module outline:

```hsp
#module

#deffunc sample_reset
value = 0
return

#defcfunc sample_value
return value

#global
```

## OpenHSP Repository Hints

- General samples live under `sample/`.
- Shared headers/modules live under `common/`.
- Help source files live under `hsphelp/` and `hsphelp_en/`.
- HSP3Dish and Emscripten assets also appear under `src/hspcmp/emscripten/assets/`.
- Compiler/runtime comparison fixtures live under `test/test_chsp_compare/gen/`; keep generated-test style consistent when editing there.

## Validation

- Prefer an existing local test for the touched area. In OpenHSP, inspect nearby `test/` scripts or build/test commands before inventing a new validation path.
- For syntax-only changes, compare against nearby examples using the same runtime and include files.
- When no HSP runtime or build command is available, state that the script was reviewed statically only.

## Common Mistakes To Avoid

- Do not write JavaScript/C/Python syntax such as braces for blocks, `==` assignment, or `function` declarations. `//` and `/* ... */` are valid HSP comments, but they do not make other C-like syntax valid.
- Do not assume `cnt` keeps its value outside the loop where it is used.
- Do not use GUI commands in HSPCL examples unless the user explicitly targets a GUI-capable runtime.
- Do not use HSP3Dish/HGIMG4 commands without the expected include and initialization pattern.
- Do not change sample asset paths casually; many examples rely on repository-relative layout.
