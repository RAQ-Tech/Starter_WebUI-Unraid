# AGENTS.md

This starter is intended to be cloned into future Python + WebUI Docker projects, especially for Unraid.

## Project goals
- Keep internal app port fixed at `3000`.
- Treat `/config` as the primary persistent path for settings and app state.
- Treat `/data` as optional storage for outputs/working files.
- Keep dependencies light and implementation easy to extend.

## Guardrails for future edits
1. Do not hardcode secrets. Use environment variables.
2. Keep `/health` route functional and fast.
3. Keep the app runnable with `docker compose up --build`.
4. Keep the UI lightweight (HTML/CSS/JS) unless a framework is explicitly required.
5. If adding new stateful features, persist to `/config` first unless there is a clear reason to use `/data`.
6. Preserve Unraid-friendly mappings in `unraid/template.xml` and `README.md`.

## Layout
- `app/main.py`: Flask app routes and config loading.
- `app/templates/`: server-rendered HTML templates.
- `app/static/`: frontend CSS/JS assets.
- `unraid/template.xml`: Unraid Community Apps template scaffold.

## Reuse checklist for new repos
- Rename app/container/image references.
- Update environment variable defaults.
- Update Unraid metadata (template URL/icon/project links).
- Keep internal container port at `3000`.
