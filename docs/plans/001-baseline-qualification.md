# 001 Starter baseline and qualification

Status as of 2026-10-12: source scaffold present; runtime and installation readiness
remain unverified. This is the project's first recorded plan, created from the
current source, README, and AGENTS.md. It has no predecessor or imported completion
history. Existing work is credited only where the stated check is evidenced.

## Current scope and stopping condition

The current request authorizes this plan and a Houston status report, with
documentation changes only. It does not authorize the future implementation,
installation, or qualification work listed below. Stop this request after the plan
is validated and delivered, and Houston's check-in is prepared or its exact failure
is explained. A prepared check-in is not a received Houston report: the real turn
completion transports it.

The plan measures readiness of the existing reusable Python and lightweight WebUI
starter. Preserve internal port `3000`, `/config` as the primary persistent mapping,
environment-driven configuration, the fast `/health` endpoint, light dependencies,
and the Docker Compose workflow. Generic installation examples stay generic.
Adding application features, authentication, a frontend framework, a new deployment,
or public exposure is outside this baseline scope. An unmet check records work to
qualify or correct later; it is not permission to do that work now.

```houston-plan-v1
{
  "id": "starter-webui-baseline-qualification",
  "revision": 1,
  "previous_plan_id": null,
  "anchor": "001-starter-baseline-and-qualification",
  "scope": "Record and qualify the existing reusable Python and lightweight WebUI starter: source contracts, Docker and browser journeys, /config storage boundary, adapted Unraid installation, artifact availability, and owner acceptance. Current authorization is documentation and reporting only; application and deployment changes require a later request.",
  "purpose": "Make the starter's evidenced capabilities and remaining readiness checks explicit without treating source presence as a working installation.",
  "milestone": "A reusable starter with evidenced container startup, health, configuration behavior, durable storage mapping, usable adapted Unraid installation, traceable image delivery, and separate owner acceptance.",
  "scope_changes": ["Initial plan established from the existing project; no predecessor, task removals, application changes, or deployment work."],
  "removed_task_ids": []
}
```

## Acceptance and next actions

Checked items below are satisfied at the stated evidence level. Unchecked items are
unverified or an identified source gap, not necessarily a failed execution. Parent
tasks remain incomplete until all their acceptance checks are satisfied. Count only
leaf checks; their count is acceptance coverage, not a measure of usable product
completion. Task IDs normalize to `task-A01` through `task-A06` in Houston.

- [x] A01 Source and plan baseline: source inventory, requirements, and normalized plan are recorded and validated.
  <!-- houston-task {} -->
  - [x] A01.1 Inventory identifies routes, UI, environment variables, Docker definitions, storage mappings, publication workflow, and reusable installation documentation without changing the app.
  - [x] A01.2 This plan parses with Houston's supported checklist grammar, satisfies its plan-facts schema, and preserves every defined check and dependency.

- [ ] A02 Container and web behavior: the existing application works through the documented local container and browser journeys.
  <!-- houston-task {"state":"underway","owner":"codex","action":"On a later qualification request, build and start an isolated container and exercise the web journeys; preserve existing containers and data.","depends":["A01"]} -->
  - [x] A02.1 Source implements the homepage, GET /health, and GET /api/info with environment-driven metadata and a lightweight server-rendered interface.
  - [x] A02.2 Docker and Compose define internal port 3000, configurable host port 8080 by default, and a health probe with a three-second request timeout.
  - [ ] A02.3 The documented docker compose up --build journey succeeds with isolated empty appdata and produces a running container on the selected host port.
  - [ ] A02.4 Runtime homepage, information API, and /health responses are successful; the health response reports healthy and completes within the configured probe timeout.
  - [ ] A02.5 Changed environment values affect the runtime metadata and example feature flag after container recreation; placeholder logging is described accurately.
  - [ ] A02.6 The actual homepage is inspected in desktop and narrow browser views for readable layout and usable content; a static Healthy label is not used as live-health evidence.
  - [x] A02.7 The two open low-severity Flask advisories are reviewed against actual starter behavior and receive an evidenced fix or documented disposition before release qualification is claimed.

- [ ] A03 Storage boundary and persistence: /config is usable durable storage, and claims match the application's actual state behavior.
  <!-- houston-task {"state":"underway","owner":"codex","action":"On a later qualification request, verify /config write access and a disposable marker surviving container recreation in isolated appdata; do not claim saved application settings that the starter does not implement.","depends":["A02"]} -->
  - [x] A03.1 Docker, Compose, and the Unraid scaffold consistently identify /config as the primary persistent container path.
  - [x] A03.2 The source boundary is documented: CONFIG_PATH is read and displayed, but no settings/state write-and-reload feature currently exists.
  - [ ] A03.3 The container can read and write a disposable marker in an isolated mapped /config directory with the documented mapping permissions.
  - [ ] A03.4 The marker survives restart and recreation of that test container; evidence distinguishes volume durability from saved application settings.

- [ ] A04 Adapted Unraid installation: a representative cloned starter has accurate metadata and passes the native DockerMan installation journey.
  <!-- houston-task {"state":"underway","owner":"codex","action":"On a later installation qualification request, adapt a disposable copy's generic references, resolve icon/favicon gaps within authorized scope, and verify the native DockerMan journey without changing unrelated workloads.","depends":["A02","A03","A05"]} -->
  - [x] A04.1 README and template describe the same internal port 3000, configurable host port, /config appdata mapping, and example environment variables.
  - [ ] A04.2 The clone's image, support, project, template, and icon references resolve to its actual intended resources; generic placeholders are not mistaken for an installable release.
  - [ ] A04.3 The Unraid icon and browser favicon actually render using appropriate accessible assets; missing or unwired source assets are resolved before this check passes.
  - [ ] A04.4 Installation through a durable DockerMan template with isolated empty appdata opens the WebUI and a successful /health response using the documented mappings.
  - [ ] A04.5 Edit, WebUI, Force Update, autostart controls, and container recreation are verified in the native interface while preserving the test mapping and data.

- [ ] A05 Artifact delivery: container publication and usable artifact identity are traceable separately from source and deployment.
  <!-- houston-task {"state":"underway","owner":"codex","action":"On a later delivery qualification request, inspect the intended published image and access policy, record its tag/digest and source lineage, and test pulling and starting that exact artifact.","depends":["A01"]} -->
  - [x] A05.1 The source defines a GHCR build-and-push workflow for main, version tags, and manual dispatch; its historical success is recorded separately below.
  - [ ] A05.2 The intended image tag and digest can be resolved and pulled using the intended access policy without changing visibility to bypass access problems.
  - [ ] A05.3 The exact pulled image starts and passes /health, with source, build result, published digest, and tested artifact identities linked in the evidence.

- [ ] A06 Owner acceptance: Chris confirms that the qualified starter is practical to clone and use after the technical checks pass.
  <!-- houston-task {"state":"not_started","owner":"chris","action":"After the technical qualification tasks are satisfied, review the documented cloning and installation journey and confirm practical usability or list remaining issues.","depends":["A02","A03","A04","A05"]} -->
  - [ ] A06.1 Chris has reviewed a qualified representative clone and accepted its reuse and installation experience; source inspection, automation, and synthetic actors cannot satisfy this check.

## Current evidence

| Evidence | Observation | Limit |
|---|---|---|
| Source baseline | Inspected application-source baseline is `6479a8c70ebc0f2a391174fe7fb78caab79b5d6c`. The previous local revision `17b1a6b5fe409f06a7521b8c01de8e010a991753` has the identical repository tree; the intervening icon addition was reverted. | This identifies inspected source, not a deployed version. |
| Web source | `app/main.py`, `app/templates/index.html`, and `app/static/styles.css` contain three routes and a responsive CSS shell. `app/requirements.txt` pins Flask 3.1.3 (3.1.0 until 2026-11-04). | No runtime or visual browser checks were executed for this request. The homepage's Healthy wording is static. |
| Container source | `Dockerfile` uses Python 3.15-slim (3.12-slim until 2026-11-04) and port 3000; `docker-compose.yml` maps the host port and /config and defines a health probe. | No build, start, empty-appdata, writable-volume, or recreation test was executed for this request. |
| Storage boundary | `CONFIG_PATH` is environment metadata. The inspected app does not save or reload settings/state. | The README's broad settings-persistence wording must not be treated as an implemented capability. |
| Installation source | `README.md` and `unraid/template.xml` provide reusable installation instructions and generic port, path, and environment mappings. | Template identity and image links remain placeholders. No actual DockerMan installation was inspected. |
| Assets | A PNG exists under `unraid/`; the template points to a generic `docs/icon.png` URL, and no favicon is wired into the homepage. | An existing PNG or URL string does not establish rendered icon/favicon behavior. |
| Historical automation | [Publish container image run 32516564663](https://github.com/RAQ-Tech/Starter_WebUI-Unraid/actions/runs/32516564663) was observed completed with success for the inspected app-source baseline. At that revision the workflow only built and pushed; it defined no browser, health, or persistence tests. | This is historical build/push evidence, not a registry pull test, current deployment verification, or a result for later documentation commits. |
| Dependency alerts | GitHub's authenticated alerts API reports two open low-severity Flask advisories against `app/requirements.txt`: [GHSA-4grg-w6v8-c28g](https://github.com/advisories/GHSA-4grg-w6v8-c28g), with first patched version 3.1.1, and [GHSA-68rp-wp8r-4726](https://github.com/advisories/GHSA-68rp-wp8r-4726), with first patched version 3.1.3. On 2026-11-04 Flask moved to 3.1.3, which is at or above both patched versions. Review: the starter sets no `SECRET_KEY` and never uses `session`, so neither the signing-key fallback nor the missing `Vary: Cookie` issue affected its behavior. | GitHub closes alerts after it rescans the pushed manifest; check the alert state rather than assuming it. |
| Version sweep (2026-11-04) | Under the owner's 2026-11-04 rule (use the latest stable release unless a reason is recorded), pins with no recorded reason moved: base image `python:3.12-slim` to `python:3.15-slim` (Debian 13 trixie); Flask `3.1.0` to `3.1.3`; `actions/checkout` v4 to v7, `docker/setup-buildx-action` v3 to v4, `docker/login-action` v3 to v4, `docker/metadata-action` v5 to v6, `docker/build-push-action` v6 to v7. Nothing was held back. Added `.github/dependabot.yml` (pip in `/app`, docker, github-actions; weekly). The publish workflow now also runs on pull requests to `main`, builds the image, and smoke-tests the running container (`/health` reports healthy, `/api/info`, `/`, static CSS, and the image's own HEALTHCHECK command) before any push; pull requests never log in or push. A local run on Python 3.15.2 in a fresh environment installed Flask 3.1.3 with Werkzeug 3.1.9, passed `pip check`, and passed `/health`, `/api/info`, `/`, static CSS, and 404 checks through Flask's test client. | The local check used no container. The container build and smoke test run in GitHub Actions; their result belongs to that run. Neither is a Compose, empty-appdata, persistence, or Unraid installation check, so A02.3 to A02.6 and later tasks stay open. |
| Plan validation | The complete checklist is normalized using Houston's local parser and checked against its PlanFacts schema before reporting. | Normalization validates reporting structure; it does not qualify the app. |

## Unknowns, gaps, and sequence

No runtime failures were observed because runtime checks were not performed.
Container startup, live route health, visual usability, storage permissions,
restart/recreation persistence, usable image tag/digest, adapted Unraid installation,
deployment identity/current health, and owner acceptance remain unverified. No
deployment target, private credentials, or installation-specific values are
included or inferred. Existing repository visibility is preserved.

The two low-severity Flask advisories were reviewed and fixed on 2026-11-04 by
moving Flask to 3.1.3 (see the version sweep row). Neither affected the starter's
behavior, because it uses no signing key or session.

Source gaps are explicit: no saved-settings feature, no wired favicon, and generic
Unraid resource links. Generic links are intentional scaffold values requiring
adaptation in a clone. Do not add a settings feature merely to qualify the storage
mapping; keep its capability boundary truthful.

Recommended future order: A02 container/web qualification, A03 storage qualification,
A05 artifact qualification, A04 adapted Unraid qualification, then A06 owner review.
No immediate owner action or access request is necessary to finish the current
documentation/reporting task. Future tasks are eligible only under a later request.
There is no existing deployment or acceptance evidence in this plan to claim as
verified. No task is marked blocked merely because its qualification is unrun.

## Reporting and resume

This Markdown file is the authoritative plan. Houston receives normalized facts
from these IDs and checks, with the selected Simple, Expanded, and Technical
narratives sharing the same evidence and limitations. Keep the plan revision at 1
for this initial baseline; later scope changes must be explicit. Do not infer a
previous report, plan revision, or completion percentage from the source inventory.

For a reporting-only follow-up, re-read this plan and the current source, extract
the complete normalized facts, and use the lifecycle connector's exact active turn
context. Check the current receipt separately after real completion when needed;
staging alone never establishes delivery. Update this file only for verified new
evidence or an authorized scope change.
