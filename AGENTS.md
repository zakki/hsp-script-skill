# Agent Development Notes

This repository develops the `hsp-script` Codex skill. Keep skill changes evidence-driven and avoid rewriting guidance from guesswork.

## Development Policy

- When a weakness in the skill is found, first isolate the specific HSP feature, command, runtime behavior, or validation issue involved.
- Create or update a small sample under `test/` that exercises the problematic feature directly. Keep the sample narrow enough that compiler or runtime output points to the behavior being studied.
- Validate the sample with the closest available HSP/OpenHSP tool before changing the skill guidance. For local OpenHSP compiler checks, use `hspcmp` with the appropriate `--compath=<OpenHSP-root>/common/` when needed.
- Treat compiler errors and warnings as evidence. Do not replace working HSP idioms just because an earlier command was missing include paths, runtime options, or package context.
- After the behavior is understood, update `skills/SKILL.md` only for core workflow changes. Put detailed syntax, runtime, validation, and package-layout lessons in `skills/references/hsp-notes.md`.
- Keep user-facing examples portable. Do not write machine-specific absolute paths into README files or skill guidance; use placeholders or environment variables such as `$OPENHSP_ROOT`.
- Leave unrelated sample files and generated artifacts alone. If validation creates temporary files such as `obj`, `hsptmp`, or `.ax`, remove them unless they are intentionally part of a checked-in fixture.

## Expected Loop

1. Reproduce or probe the issue with a minimal HSP sample.
2. Compile or run it with the relevant HSP runtime/tooling.
3. Read the output and identify the root cause.
4. Update the skill notes only with what the sample demonstrated.
5. Re-run the validation command and inspect the final diff.
