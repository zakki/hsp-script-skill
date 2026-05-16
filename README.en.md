# hsp-script

Codex skill for writing, editing, reviewing, and explaining Hot Soup Processor scripts for HSP3/OpenHSP.

## Scope

- Standard HSP3 windowed scripts
- HSPCL console scripts
- HSP3Dish scripts
- HGIMG4 scripts
- `.as` module files
- OpenHSP sample, help, and test code

This skill helps Codex keep HSP-specific style and conventions in mind, including labels, `repeat`/`loop`, `gosub`, command-style statements, HSP preprocessor directives, the Windows HSP package layout, and OpenHSP repository layout conventions.

The primary target is the official Windows HSP 3.7 package, which is likely the most common user environment. The skill treats `hsed3.exe`, `hspcmp.exe`, `hsp3.exe`, `hsp3cl.exe`, `hsp3dish.exe`, `common/`, `sample/`, `doclib/`, and `hsphelp/` as the normal reference layout. Linux+OpenHSP source-tree usage is documented as a supplementary development and verification environment.

## Installation

Clone this repository into your Codex skills directory:

```bash
git clone https://github.com/<user>/hsp-script.git ~/.codex/skills/hsp-script
```

Restart Codex or reload skills if your environment requires it.

## Usage

Mention HSP, HSP3, OpenHSP, `.hsp`, or `.as` work in your prompt. You can also invoke the skill explicitly:

```text
Use $hsp-script to write a small HSP3 windowed sample.
```

Example prompts:

```text
HSP3で簡単な時計スクリプトを書いて
```

```text
Use $hsp-script to review this .hsp file for syntax issues.
```

```text
Create a touch input sample for OpenHSP sample/hsp3dish.
```

## Files

- `SKILL.md`: Codex-facing skill instructions and trigger description.
- `references/hsp-notes.md`: HSP syntax notes, examples, runtime guidance, and OpenHSP repository hints.
- `agents/openai.yaml`: UI metadata for skill lists.
- `README.md`: Japanese README.

## Notes

This repository is intended to be installed as a single skill folder. The repository root should contain `SKILL.md`.
