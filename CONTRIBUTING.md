# Contributing to quarantine

Thanks for your interest in contributing! quarantine is in early development, which means contributions have outsized impact — and also that things move fast. This guide covers how to get involved without friction.

## Ways to contribute

- **Report bugs** — open an issue with steps to reproduce, expected vs. actual behavior, and your environment (OS, Docker version, hardware).
- **Suggest features** — open an issue describing the problem you're solving, not just the solution. Discussion happens before code.
- **Improve docs** — unclear instructions are bugs. PRs that fix wording, add examples, or clarify setup steps are always welcome.
- **Contribute code** — see the workflow below.

## Development setup

```bash
git clone https://github.com/QuarantineAl/platform.git
cd platform
```

Prerequisites:

- Docker Engine with Compose v2 (`docker compose version`)
- `age` and `sops` for secrets handling
- A Linux host or VM (the platform targets Linux servers; macOS works for most development)

Copy `.env.example` to `.env` and adjust values for your environment. Never commit your `.env` — it's gitignored for a reason.

## Branching and workflow

We use a simple two-branch model:

- **`main`** — stable. What people should run.
- **`develop`** — integration branch. Feature work lands here first.

Both branches are protected: **no direct pushes, all changes go through pull requests.**

1. Fork the repo (or create a branch if you have write access).
2. Branch off `develop`:
   ```bash
   git checkout develop
   git checkout -b feat/my-change
   ```
3. Make your changes.
4. Open a PR **targeting `develop`** (not `main`).

Branch naming: `feat/…`, `fix/…`, `docs/…`, `chore/…` — short and descriptive.

## Commit messages

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
feat(traefik): add wildcard cert resolver for internal services
fix(zitadel): correct healthcheck endpoint path
docs: clarify age key generation step
```

Keep the subject under ~72 characters; use the body to explain *why* when it isn't obvious.

## Pull request guidelines

- Keep PRs focused — one logical change per PR. Small PRs get reviewed fast; big ones stall.
- Describe **what** changed and **why**. Link related issues (`Closes #123`).
- If your change touches service configuration, note how you tested it (e.g. "brought the stack up clean on Ubuntu 24.04, verified Traefik routes").
- Update documentation in the same PR when behavior changes.
- CI must pass before merge.

## Configuration conventions

A few project-wide rules to keep the stack consistent:

- **Compose files**: one service per directory, following the existing layout. Reuse the shared networks and the shared PostgreSQL instance rather than adding per-service databases.
- **Routing**: expose services via Traefik labels, never by publishing host ports directly (except Traefik itself).
- **Secrets**: anything sensitive goes through SOPS + age. Plaintext secrets in compose files or committed `.env` files will fail review.
- **Observability**: new services should ship logs/metrics/traces to the shared OpenTelemetry pipeline where the service supports it.

## Reporting security issues

Please **do not** open public issues for security vulnerabilities. See [SECURITY.md](SECURITY.md) for how to report them privately.

## Questions?

Open a [discussion](https://github.com/QuarantineAl/platform/discussions) — there are no stupid questions, only missing docs.