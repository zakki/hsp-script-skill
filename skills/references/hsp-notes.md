# HSP Notes

## Target Environment

Use the official Windows HSP 3.7 package as the main assumption for user-facing scripts. In that layout:

- `hsed3.exe` / `hsed3_en.exe`: HSP Script Editor.
- `hspcmp.exe`: compiler.
- `hsp3.exe`, `hsp3_64.exe`, `hsp3utf.exe`: standard desktop runtimes.
- `hsp3cl.exe`: console runtime.
- `hsp3dish.exe`: HSP3Dish runtime.
- `hsp3gp.exe`, `hsp3gpdx.exe`, `hsp3hg.exe`, `hsp3dh.exe`: game/graphics-related runtimes or helpers.
- `runtime/*.hrt`: runtime definition files such as `hsp3cl.hrt`, `hsp3dish.hrt`, `hsp3gp.hrt`, and `hsp3_64.hrt`.
- `common/`: standard include files and module headers, including Windows plugin headers such as `user32.as`, `kernel32.as`, `winmm.as`, `hspinet.as`, `hspext.as`, `hspcv.as`, and `hgimg4.as`.
- `sample/`: user-facing samples grouped by feature, for example `basic`, `game`, `hspcl`, `hsp3dish`, `hgimg4`, `hgimg3`, `sprite`, `module`, `comobj`, `hspsock`, `hspinet`, `hspcv`, `hsp3utf`, `hspvoicevox`, `Artlet2D`, `SQLele`, `dotfw`, `d3module`, `gpmodule`, and `new37`.
- `doclib/`: packaged documentation such as `hsp3.htm`, `hspprog.htm`, `hsp3win.html`, `hsp3dish*.htm`, `hsp3linux_pi.html`, plugin docs, and update/history notes.
- `hsphelp/`: help source/index files used by the editor/help system.
- DLLs in the package root provide Windows plugin functionality; include matching `.as` files from `common/` when using them.

Mention Linux+OpenHSP as a source-tree/development variant, not the default end-user layout. In the OpenHSP repository, equivalent materials are split across `sample/`, `sample_ref/`, `sample_ref_pp/`, `common/`, `hsphelp/`, `hsphelp_en/`, `doclib/`, `doclib_en/`, `src/`, `test/`, and `build/`.

## Runtime Selection

- Standard HSP3: windowed desktop scripts using commands such as `screen`, `mes`, `button`, `color`, `pos`, `line`, and `stick`.
- HSPCL: console or command-line scripts; avoid GUI-only assumptions.
- HSP3Dish: portable/mobile/web-oriented scripts; start from examples under package-root `sample/hsp3dish` and include `hsp3dish.as` when needed.
- HGIMG4: 3D/game scripts; start from examples under package-root `sample/hgimg4` and include `hgimg4.as`.
- Module files: `.as` files commonly define reusable commands/functions with `#module`, `#deffunc`, `#defcfunc`, `#global`, and related preprocessor features.

## Syntax Reminders

- Comments may use `;`, `//`, or `/* ... */`. Prefer `;` in new code unless nearby code uses another style.
- Labels start with `*`, for example `*main`.
- Assignment is commonly `name = value`. Commands are usually command-first, for example `mes "text"`.
- `repeat n` starts a loop and `loop` ends it. `cnt` is the current repeat counter for the innermost loop.
- `if condition : command` is common for short branches. `if condition { ... } else { ... }` is valid in HSP3/HSPCL, but braces do not make arbitrary C-like syntax valid.
- `\` is the integer remainder operator, for example `n \ 3 = 0`.
- `!` can be used as a not-equal comparison operator, for example `if i ! hitId { ... }`.
- `goto *label` jumps; `gosub *label` calls a subroutine that returns with `return`.
- Use `stop` to stop a GUI script without closing immediately; use `end` when the program should terminate.
- Preprocessor lines begin with `#`, such as `#include`, `#const`, `#define`, `#module`, `#deffunc`, and `#defcfunc`.
- `print` is an alias of `mes`; packaged help recommends `mes`. In HSPCL, `mes` prints to the console.

## User-Defined Commands and Functions

`#deffunc` defines a command-like routine and returns with `return`. `#defcfunc` defines a function used in expressions and must return a value.

```hsp
#module

#deffunc set_var var target, int value
target = value
return

#deffunc set_array_first array target, int value
target(0) = value
return

#defcfunc sum_array_first2 array target
return target(0) + target(1)

#defcfunc scratch_once int value, local scratch
scratch = scratch + value
return scratch

#global
```

Parameter-type reminders:

- `int`, `double`, and `str` receive values.
- `var` receives the exact variable reference supplied by the caller. If called as `set_var values(1), 42`, assignment to `target` changes `values(1)`.
- `array` receives the base array. If called as `set_array_first values(1), 99`, `target(0)` refers to `values(0)`, not `values(1)`.
- `local` in a parameter list is not a caller argument. It declares a temporary variable initialized for each call and discarded on return. Put it at the end of the parameter list.
- `#deffunc local name` and `#defcfunc local name` are different: this `local` makes the command/function name module-scoped. Call it as `name@module(...)`.
- For module internals, variables often appear with module qualification such as `value@module`; follow nearby module style instead of guessing scope rules.

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

Module-scoped function name:

```hsp
#module private_scope

#defcfunc local hidden_value
return 321

#global

mes hidden_value@private_scope()
```

Keyboard input pattern for simple games:

```hsp
stick k, 15
; stick bits: 1=left, 2=up, 4=right, 8=down, 16=space, 32=enter, 128=esc

left = 0
right = 0
if k & 1 : left = 1
if k & 4 : right = 1
getkey wasd, 'A'
if wasd : left = 1
getkey wasd, 'D'
if wasd : right = 1
```

Use `stick` for bundled cursor/button state and `getkey` for explicit character keys such as `A`, `D`, `W`, and `S`. The second `stick` parameter is a bitmask for keys that should keep reporting while held down.

## Windows Package Hints

- Prefer Windows package paths in user-facing explanations: `sample/basic`, `sample/hsp3dish`, `sample/hgimg4`, `common/hsp3dish.as`, `common/hgimg4.as`, and `doclib/hsp3.htm`.
- For editor-oriented users, assume they run scripts from HSP Script Editor rather than from a Unix shell.
- For plugin examples, check both the DLL in the package root and the matching header under `common/`.
- For 64-bit or UTF-8 topics, distinguish `hsp3_64.exe`/`common/hsp3_64.as` and `hsp3utf.exe`/`common/hsp3utf.as`.
- For console examples, use `hsp3cl.exe` and `common/hsp3cl.as` where relevant.
- For HSP3Dish, web, Android, or iOS topics, the Windows package also contains `hsp3js/`, `android/`, `iOS/`, and `dish_p_helper.exe`.

## HSP Help Lookup

Use packaged `hsphelp/*.hs` files as the local command reference when exact syntax, parameters, or key-code tables matter. Do not assume the path is stable. Prefer, in order:

- A user-provided HSP package or OpenHSP path.
- Nearby project/package directories containing `hsphelp/`.
- Common local source/package layouts such as `OpenHSP/hsphelp`, `OpenHSP/tmp/hsp37/hsphelp`, or package-root `hsphelp`.

Use tools that fit the user's environment. On Windows, do not assume Unix tools such as `find`, `file`, `iconv`, or `rg` are installed.

PowerShell search pattern:

```powershell
Get-ChildItem -Path $root -Recurse -Filter *.hs |
  Where-Object { $_.FullName -match '\\hsphelp\\' }
```

Unix-like shell pattern, when those tools are available:

```sh
find "$root" -path '*/hsphelp/*.hs' -print
rg -n '^%index|^stick$|^getkey$' "$hsphelp_dir"
```

Portable decode pattern, when Python is available:

```python
from pathlib import Path

data = Path(path_to_hs).read_bytes()
for enc in ("utf-8", "cp932", "shift_jis"):
    try:
        text = data.decode(enc)
        break
    except UnicodeDecodeError:
        pass
else:
    raise UnicodeDecodeError("hsphelp", data, 0, 1, "unknown encoding")
```

Encoding varies by source. OpenHSP repository files are often UTF-8, while Windows package-derived `hsphelp` files may be Shift_JIS/CP932. Try UTF-8 and CP932/Shift_JIS before trusting text output. Command names and `%index` markers are ASCII, so byte-oriented search can often locate entries before decoding; decode before quoting or relying on Japanese descriptions.

## Linux+OpenHSP Source Tree Notes

- General samples live under `sample/`, with reference/preprocessed variants under `sample_ref/` and `sample_ref_pp/`.
- Shared headers/modules live under `common/`.
- Help source files live under `hsphelp/` and `hsphelp_en/`.
- HSP3Dish and Emscripten assets also appear under `src/hspcmp/emscripten/assets/`.
- Compiler/runtime comparison fixtures live under `test/test_chsp_compare/gen/`; keep generated-test style consistent when editing there.

## Validation

- Prefer validation that matches the user's environment. For Windows package users, compile/run with HSP Script Editor or package tools such as `hspcmp.exe`, `hsp3.exe`, `hsp3cl.exe`, or `hsp3dish.exe` when available.
- In Linux+OpenHSP source work, inspect nearby `test/` scripts or build/test commands before inventing a new validation path.
- For syntax-only changes, compare against nearby examples using the same runtime and include files.
- For interactive programs, compile success is not enough: manually or programmatically check the main input paths, boundary actions, game-over/restart paths, and any array-index-heavy code.
- Clean up compiler/runtime artifacts such as `.ax`, `obj`, or `hsptmp` unless the user asked to keep generated files.
- When no HSP runtime or build command is available, state that the script was reviewed statically only.

## Common Mistakes To Avoid

- Do not write JavaScript/C/Python syntax such as `==` assignment or `function` declarations. HSP accepts `if { ... }` blocks and C-style comments, but those features do not make HSP a C-like language.
- Do not assume `cnt` keeps its value outside the loop where it is used.
- Do not use GUI-only commands in HSPCL examples unless the user explicitly targets a GUI-capable runtime; `mes`/`print` are aliases and can be used for console output under HSPCL.
- Do not use HSP3Dish/HGIMG4 commands without the expected include and initialization pattern.
- Do not change sample asset paths casually; many examples rely on package-relative or repository-relative layout.
- Do not read arrays after only setting an error flag for out-of-range coordinates. For board/collision code, guard the actual array reference with a full bounds check such as `x >= 0 & x < width & y >= 0 & y < height`.
