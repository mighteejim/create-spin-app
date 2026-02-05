# create-spin-app (Spin + Fermyon)

Codex skill for creating, building, running, deploying, and troubleshooting Spin applications.

## Contents

- `SKILL.md`: Skill definition and workflow
- `agents/openai.yaml`: UI metadata
- `references/`: Capability matrix, templates, plugins, build/run, and Fermyon Cloud deploy refs

## Prerequisites

- Spin CLI installed (`spin --version`)
- Install Spin via Homebrew:
  - `brew tap spinframework/tap`
  - `brew install spinframework/tap/spin`
- For cloud deploys: `spin cloud login` completed

## Links

- [Fermyon](https://www.fermyon.com/)
- [Fermyon Cloud Docs](https://developer.fermyon.com/cloud)
- [Spin Docs](https://spinframework.dev/)
- [Install Spin](https://spinframework.dev/v3/install)

## Install (local)

```bash
ln -s /path/to/create-spin-app ~/.codex/skills/create-spin-app
```

Restart Codex to pick up new skills.

## Notes

- Local dev + Fermyon Cloud only (CLI-only).
- No web dashboard usage.

## License

MIT
