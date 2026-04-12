# Starter WebUI Unraid (Python)

A reusable, Unraid-first Docker starter for Python backend + lightweight web UI projects.

## What this starter optimizes for
- Fast bootstrap for new app repos.
- Clean container behavior and minimal dependencies.
- Simple Unraid mapping model.
- Easy cloning/adaptation by changing only names, ports, paths, and env vars.

## Core conventions
- Internal app port is fixed: **`3000`**.
- Primary persistent path: **`/config`** (settings/state; map to Unraid `appdata`).
- Optional persistent path: **`/data`** (working files/outputs).
- Environment-variable-driven configuration.
- Health endpoint at **`/health`**.

## Project structure

```text
.
├── AGENTS.md
├── Dockerfile
├── .dockerignore
├── .env.example
├── docker-compose.yml
├── README.md
├── unraid/
│   └── template.xml
└── app/
    ├── main.py
    ├── requirements.txt
    ├── templates/
    │   └── index.html
    └── static/
        └── styles.css
```

## Quick start (local Docker)

1. Copy env example:
   ```bash
   cp .env.example .env
   ```
2. Build and run:
   ```bash
   docker compose up --build
   ```
3. Open UI:
   - `http://localhost:8080` (or your `HOST_PORT`)
4. Health check:
   - `http://localhost:8080/health`

## Environment variables

| Variable | Default | Purpose |
|---|---|---|
| `APP_NAME` | `Starter WebUI App` | UI/API app display name |
| `APP_ENV` | `production` | Environment label |
| `LOG_LEVEL` | `info` | Logging placeholder |
| `FEATURE_PLACEHOLDER` | `true` | Example feature flag |
| `HOST_PORT` | `8080` | Host-exposed port mapped to container `3000` |
| `CONFIG_PATH` | `/config` | Primary persistent config/state path in container |
| `DATA_PATH` | `/data` | Optional working/output path in container |

## Unraid deployment notes

### Typical mapping in Unraid
- Port mapping: host port (choose any free port) -> container port **`3000`**
- Primary path mapping (required):
  - Host: `/mnt/user/appdata/<your-app-name>`
  - Container: `/config`
- Optional data mapping:
  - Host: `/mnt/user/data/<your-app-name>` (or another share)
  - Container: `/data`

Use `unraid/template.xml` as the base Community Apps template.

## What to edit first when cloning this starter
1. **App/repo identity**
   - Rename repo, update image/repository references in `unraid/template.xml`.
2. **Container naming**
   - Update `container_name` in `docker-compose.yml`.
3. **Host port**
   - Change `HOST_PORT` in `.env` for each deployment.
4. **Persistent paths**
   - In Unraid, map `/config` to appdata path first.
   - Map `/data` only if your app needs output storage.
5. **Runtime config**
   - Add your project-specific env vars to `.env.example`, compose, and docs.

## Included starter behavior
- Homepage (`/`) with:
  - app name
  - healthy status indicator
  - config/env placeholders
  - expandable feature workspace section
- Health endpoint (`/health`) for healthchecks
- Example API route (`/api/info`)
- Lightweight modern CSS shell

## Security and secrets
- Do not hardcode secrets in source files.
- Pass secrets using environment variables or external secret managers.

## Next extension ideas
- Add structured logging and request IDs.
- Add auth middleware.
- Add a module layout under `app/` for domain features.
- Add optional SQLite/Postgres integration with `/config` defaults.
