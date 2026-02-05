# spin-deploy (Spin + Fermyon)

Codex skill for creating, building, running, deploying, and troubleshooting Spin applications.

## What Is A Spin App?

Spin apps are small, composable WebAssembly services designed for fast startup, low memory use, and straightforward local-to-cloud workflows. They are a strong fit for APIs, webhooks, and background tasks where you want quick iteration and predictable performance without heavyweight runtime overhead.

## Why Deploy To Fermyon Cloud?

Fermyon Cloud is the native home for Spin apps: low-latency global edge deployment, fast cold starts, and a CLI-first workflow that matches local development. Deploy with `spin cloud deploy` and get a public URL quickly, without changing your app structure.

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
ln -s /path/to/spin-deploy ~/.codex/skills/spin-deploy
```

Restart Codex to pick up new skills.

## Install (Codex $skill-installer)

From Codex, use $skill-installer and a GitHub directory URL. Example:

```
$skill-installer install https://github.com/mighteejim/spin-deploy
```

## Notes

- Local dev + Fermyon Cloud only (CLI-only).
- No web dashboard usage.

## License

MIT
