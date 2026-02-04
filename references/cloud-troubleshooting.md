# Fermyon Cloud Troubleshooting

- Auth error or 401: run `spin cloud login` again.
- `spin cloud` unknown: install the cloud plugin, then retry.
- Build/deploy failure: run `spin build`, then re-run `spin cloud deploy --build`.
- Missing config/variables: re-run `spin cloud variables set` for each key.
