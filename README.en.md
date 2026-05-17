# hsp-script

Skill for writing, editing, reviewing, and explaining Hot Soup Processor scripts for HSP3/OpenHSP. Works with both Codex and Claude Code.

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

### Codex

Clone this repository into any working directory, then symlink the repository's `skills/` directory into your Codex skills directory:

```bash
git clone https://github.com/<user>/hsp-script-skill.git ~/git/hsp-script-skill
mkdir -p ~/.codex/skills
ln -s ~/git/hsp-script-skill/skills ~/.codex/skills/hsp-skills
```

If `~/.codex/skills/hsp-skills` already exists as a directly cloned repository directory, move it aside or remove it before creating the symlink.

Restart Codex or reload skills if your environment requires it.

### Claude Code

Clone this repository into any working directory, then symlink the repository's `skills/` directory into your Claude Code personal skills directory:

```bash
git clone https://github.com/<user>/hsp-script-skill.git ~/git/hsp-script-skill
mkdir -p ~/.claude/skills
ln -s ~/git/hsp-script-skill/skills ~/.claude/skills/hsp-script
```

The skill is recognized as `~/.claude/skills/hsp-script/SKILL.md` and is available across all projects. To use on a per-project basis, symlink into the project-root `.claude/skills/` instead of `~/.claude/skills/`.

Changes to `SKILL.md` are picked up live within the current session (no restart needed). A restart is only required when creating the symlink for the first time.

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

- `AGENTS.md`: Development policy for agents updating this skill repository.
- `skills/SKILL.md`: Codex-facing skill instructions and trigger description.
- `skills/references/hsp-notes.md`: HSP syntax notes, examples, runtime guidance, and OpenHSP repository hints.
- `skills/agents/openai.yaml`: UI metadata for skill lists.
- `README.md`: Japanese README.

## Notes

Codex should load the `skills/` directory, not the repository root. Do not place the repository itself directly at `~/.codex/skills/hsp-skills`; place a symlink there that points to `hsp-script-skill/skills`.
