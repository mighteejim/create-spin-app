---
name: spin-deploy
description: Create, build, run, deploy, and troubleshoot Spin applications. Use for requests to scaffold a Spin app, pick a language or template based on capability requirements, install or update templates/plugins, run `spin build`, `spin up`, or `spin watch`, deploy with `spin cloud deploy`, manage Fermyon Cloud variables, and diagnose issues with `spin doctor` or `spin cloud`.
---

# Create Spin App

## Overview

Create local Spin apps from templates, select language by required capabilities, build/run locally, and optionally deploy to Fermyon Cloud with the Spin CLI.

## Local Docs First

Use `references/*` as the source of truth. Prefer `spin <cmd> --help` to confirm flags. Avoid web search unless the user explicitly asks or a required detail is missing from references/help.

When implementing app code, read `references/sdk-apis.md` for main SDK calls and manifest hints.

## Interactive CLI Notes

`spin new` prompts for app name even with `--accept-defaults` and requires a TTY. Use a TTY session or `--init` in the target directory.

## Quick Decision Trees

Need a trigger?
`HTTP -> Rust | JS/TS | Python | TinyGo`
`Redis -> Rust | Python | TinyGo (not JS/TS)`
`Custom triggers -> Rust only`

Need MQTT?
`MQTT -> Rust or JS/TS`

Need everything + safest option?
`Pick Rust (full capability set + custom triggers).`

## Intent Translation (Defaulting Rules)

Infer requirements from the user's goal. Avoid asking for trigger/capabilities unless intent is ambiguous.

Trigger defaults:
- User-facing app, API, webhook, UI, CRUD -> HTTP trigger.
- Redis-driven workload (streams, pub/sub, keyspace events) -> Redis trigger.
- Anything else -> HTTP unless explicitly non-HTTP/Redis.

Capability defaults:
- "Store data", "bookings", "accounts", "inventory" -> add a database.
  - Default to SQLite for local/dev unless user names MySQL/Postgres.
- "Cache/queue" -> outbound Redis.
- "Call an API", "integrations" -> outbound HTTP.
- "IoT", "device messaging" -> MQTT (Rust or JS/TS).
- "AI summarization/embeddings/chat" -> AI capability.

Language defaults:
- Honor user language preference if supported.
- If ambiguous or mixed requirements, choose Rust (most capable).

Ask only for missing, decision-critical details:
project name, language preference (if multiple valid), database choice (if not implied), and any required integrations.

Deployment defaults:
- "Deploy", "host", "public URL" -> Fermyon Cloud (CLI). Ask only if they want another provider.

## Capability Index (Spin APIs)

### Triggers

Capability | Supported SDKs | Reference
--- | --- | ---
HTTP | Rust, JS/TS, Python, TinyGo | `references/language-support.md`
Redis | Rust, Python, TinyGo | `references/language-support.md`
Custom triggers | Rust only | `references/language-support.md`

### Built-in APIs

Capability | Supported SDKs | Reference
--- | --- | ---
Outbound HTTP | All SDKs | `references/language-support.md`
Variables | All SDKs | `references/language-support.md`
KV | All SDKs | `references/language-support.md`
SQLite | All SDKs | `references/language-support.md`
MySQL | All SDKs | `references/language-support.md`
Postgres | All SDKs | `references/language-support.md`
Outbound Redis | All SDKs | `references/language-support.md`
AI | All SDKs | `references/language-support.md`
MQTT | Rust, JS/TS | `references/language-support.md`

## Reference Map

- Language + capability selection: `references/language-support.md`
- Templates list + installs: `references/templates.md`
- Plugins (search/install): `references/plugins.md`
- Build/run/watch: `references/build-run.md`
- SDK main APIs: `references/sdk-apis.md`
- Troubleshooting: `references/troubleshooting.md`
- Fermyon Cloud auth + plugin: `references/cloud-auth.md`
- Fermyon Cloud deploy: `references/cloud-deploy.md`
- Fermyon Cloud variables: `references/cloud-variables.md`
- Fermyon Cloud troubleshooting: `references/cloud-troubleshooting.md`

## Workflow

1. Translate intent to requirements.
Infer trigger/capabilities from the goal using the defaults above. Ask only for missing decision-critical details (project name, language preference, database choice, required integrations).

2. Choose language.
Use `references/language-support.md` to map requirements to a supported SDK. If multiple options fit, prefer user language; otherwise pick Rust. If a requested capability is unsupported, propose a compatible language.

3. Ensure templates and plugins.
List templates with `spin templates list`. If missing, install official template repos from `references/templates.md`. For toolchain plugins, search and install per `references/plugins.md`.

4. Scaffold app.
Use `spin new -t <template> <name> --accept-defaults` (TTY required). Use `--value` or `--values-file` for template parameters. Use `spin add` to add components to existing apps.

5. Build and run.
Use `spin build`, `spin up --build`, or `spin watch`. See `references/build-run.md`.

6. Deploy to Fermyon Cloud (optional).
If user asks to deploy, ensure `spin cloud` is available, run `spin cloud login`, then `spin cloud deploy --build`. Manage variables if needed. See `references/cloud-auth.md`, `references/cloud-deploy.md`, `references/cloud-variables.md`.

7. Troubleshoot.
Run `spin doctor` for local issues. Use Fermyon Cloud troubleshooting when deploying. See `references/troubleshooting.md` and `references/cloud-troubleshooting.md`.

## Constraints

Local dev + Fermyon Cloud only. CLI-only (no web dashboard). Do not edit app code unless asked. If asked to deploy elsewhere, ask for guidance.

## References

`references/language-support.md`
`references/templates.md`
`references/plugins.md`
`references/build-run.md`
`references/troubleshooting.md`
`references/cloud-auth.md`
`references/cloud-deploy.md`
`references/cloud-variables.md`
`references/cloud-troubleshooting.md`
