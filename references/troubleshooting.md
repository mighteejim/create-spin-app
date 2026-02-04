# Troubleshooting

- Run `spin doctor`.
- Template missing: `spin templates list`, then install missing repo from `references/templates.md`.
- Plugin missing: `spin plugins update`, then `spin plugins install <name> --yes`.
- JS/TS builds: ensure the `js2wasm` plugin is installed.
- Python builds: `componentize-py` replaces `py2wasm`; follow Python build docs if missing.
- If a language lacks a required capability, pick a compatible language from `references/language-support.md`.
