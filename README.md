# create-spin-app -- create, build, run, and deploy Spin apps with your favorite coding agent.

Agent skill for creating, building, running, deploying, and troubleshooting Spin applications.

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
- [Codex Skills Repo](https://github.com/openai/skills)

## Install (local)

```bash
ln -s /path/to/create-spin-app ~/.codex/skills/create-spin-app
```

Restart Codex to pick up new skills.

## Install (Codex $skill-installer)

From Codex, use $skill-installer and a GitHub directory URL. Example:

```
$skill-installer install https://github.com/mighteejim/create-spin-app
```

## Notes

- Local dev + Fermyon Cloud only (CLI-only).
- No web dashboard usage.

## License

MIT
