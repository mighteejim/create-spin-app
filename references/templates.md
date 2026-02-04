# Templates

List installed templates:
`spin templates list`

Install or upgrade official template repos:

Spin repo (Rust, Go, misc):
`spin templates install --git https://github.com/spinframework/spin --upgrade`

Python:
`spin templates install --git https://github.com/spinframework/spin-python-sdk --upgrade`

JavaScript and TypeScript:
`spin templates install --git https://github.com/spinframework/spin-js-sdk --upgrade`

Notes
- `spin templates install` expects a repo with a `templates/` directory.
- Supported sources: `--git`, `--dir`, `--tar`. Optional `--branch` to target a specific tag or branch.
- After install, re-run `spin templates list` and pick the template id for `spin new` or `spin add`.
