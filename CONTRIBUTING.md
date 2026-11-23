# Contributing to quarantine

Thanks for your interest in contributing! quarantine is in early development, so contributions have outsized impact, and things move fast. This guide covers how to get involved without friction.

## Ways to contribute

- **Report bugs**: open an issue with steps to reproduce, expected vs. actual behavior, and your environment (OS, Docker version, hardware).
- **Suggest features**: open an issue describing the problem you're solving, not just the solution. Discussion happens before code.
- **Improve docs**: unclear instructions are bugs. PRs that fix wording, add examples, or clarify setup steps are always welcome.
- **Contribute code**: see the workflow below.

## Development setup

```bash
git clone https://github.com/QuarantineAl/platform.git
cd platform
```

Prerequisites:

- Docker Engine with Compose v2 (`docker compose version`)
- `age` and `sops` for secrets
- `shellcheck`, which CI runs on every shell script
- A Debian or Ubuntu host or VM to actually run the stack. macOS works for editing and `docker compose config` checks.

To stand up a real environment, follow the [platform README](https://github.com/QuarantineAl/platform#quickstart): `install.sh`, then `quarantine init` and `quarantine start`. There is no `.env` file to copy: `init` writes the environment's config, and each environment's apps and secrets live in `environments/<env>/manifest.yaml` and `secrets.sops.yaml`.

## Branches

Not every repo uses the same model. Check the default branch before you branch.

- **platform** and **docs**: trunk-based. Branch off `main` and open your PR against `main`.
- **App repos** (lazzaretto, kujtime, bem, delivery-note-ai, ...): branch off `develop` and open your PR against `develop`. A merge to `develop` deploys to the dev environment; `main` is what runs in prod.

Every change goes through a pull request, never a direct push to `main` or `develop`. On platform this is enforced by branch protection.

Branch names: `feat/…`, `fix/…`, `docs/…`, `chore/…`, short and descriptive.

## Commit messages

Write the subject as a short imperative sentence that says what the change does, for example:

```
Add bem to the catalog and enable it in dev
Pass --env-file to the PR sandbox's docker compose up
```

Keep it under ~72 characters. Use the body to explain *why* when it isn't obvious.

## Pull request guidelines

- Keep PRs focused: one logical change per PR. Small PRs get reviewed fast; big ones stall.
- Describe **what** changed and **why**. Link related issues (`Closes #123`).
- If your change touches service configuration, say how you tested it (e.g. "brought the stack up clean on Ubuntu 24.04, verified the Traefik routes").
- Update documentation in the same PR when behavior changes.
- CI must pass before merge. On platform that means `lint-and-validate` (shellcheck plus `docker compose config` across every profile) and `verify-secrets-encrypted`.

## Platform conventions

A few rules that keep the stack consistent:

- **Apps come from the catalog.** Every deployable app has an entry in `catalog.yaml` and a compose fragment under `apps/first-party/` or `apps/third-party/`. Add a new one with `scripts/new-app.sh` (see `docs/adding-an-app.md`), then switch it on per environment with `quarantine app add`.
- **Routing**: expose services through Traefik labels on the shared `edge` network. Never publish host ports directly (Traefik itself is the only exception).
- **Databases**: set `needs_db: true` and use the shared PostgreSQL instance rather than adding a database container per app.
- **Sign-in**: set `needs_oidc: true` and let the platform create the Zitadel client. Apps without native OIDC sit behind their own oauth2-proxy instance.
- **Secrets**: anything sensitive goes in `secrets.sops.yaml`, encrypted with that environment's own age key. Plaintext secrets in compose files will fail review, and CI rejects an unencrypted secrets file.
- **Observability**: new services should send logs, metrics and traces to the shared OpenTelemetry collector where they support it.

## Deploying from an app repo

App repos deploy through GitHub Actions on the org's self-hosted runners (`[self-hosted, quarantine-dev]` or `quarantine-prod`). This repo hosts the shared, reusable workflows for that; see the [README](README.md) for what each one does and how to call it.

## Reporting security issues

Please **do not** open public issues for security vulnerabilities. Contact the QuarantineAl maintainers privately instead, and include enough detail to reproduce the problem.

## Questions?

Open an [issue](https://github.com/QuarantineAl/platform/issues). There are no stupid questions, only missing docs.
