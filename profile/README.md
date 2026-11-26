<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/QuarantineAl/.github/main/profile/readme-header-dark.svg">
    <img src="https://raw.githubusercontent.com/QuarantineAl/.github/main/profile/readme-header-light.svg" alt="quarantine" height="56">
  </picture>
</p>

<p align="center">
  <strong>Self-hosted infrastructure that gets out of your way.</strong><br/>
  An open-source platform that stands up a production-grade stack on your own server in three commands, and the products we build on top of it.
</p>

<p align="center">
  <a href="https://quarantine.al">Website</a> ·
  <a href="https://github.com/QuarantineAl/platform">Get started</a> ·
  <a href="https://github.com/QuarantineAl/.github/blob/main/CONTRIBUTING.md">Contributing</a>
</p>

---

## Quickstart

Three commands, not thirty. On a Debian or Ubuntu host with a domain on Cloudflare DNS:

```bash
curl -fsSL https://raw.githubusercontent.com/QuarantineAl/platform/main/install.sh | sudo bash
quarantine init
quarantine start
```

`init` asks for your domain, environment and Cloudflare token. `start` brings everything up and is safe to re-run. See the [platform README](https://github.com/QuarantineAl/platform) for prerequisites and flags.

## What's inside

| Layer | Tool | Why |
|---|---|---|
| Orchestration | **Docker Compose v2** | Simple, portable, no cluster overhead |
| Reverse proxy | **Traefik v3** | Automatic TLS, label-based routing |
| Identity & SSO | **Zitadel** + oauth2-proxy | Single sign-on for every service, even ones without native OIDC |
| Database | **PostgreSQL** (shared) | One instance, many databases |
| File storage | **Garage** (S3-compatible) | Any app gets its own bucket by asking for one |
| Backups | **restic**, via `quarantine backup` | Nightly and encrypted, sent off the server; restore a whole volume or a single file |
| Observability | **SigNoz** + OpenTelemetry | Traces, metrics and logs in one place, switched on per environment |
| Deployments | **GitHub Actions** on self-hosted runners | Merge to deploy; every PR can get its own sandbox |
| Secrets | **SOPS + age** | Encrypted secrets, committed safely, one key per environment |

## Built on quarantine

| Product | What it does |
|---|---|
| **Lazzaretto** | Runs coding agents and LLMs from a browser, each session sealed in its own workspace |
| **toolkit** | Shared design system: `@quarantineal/ui`, `icons`, `design-tokens` |

## Principles

- **Three commands, not thirty.** Onboarding is measured in minutes.
- **Convention over configuration.** Sensible defaults everywhere; override only when you need to.
- **Your hardware, your data.** No vendor lock-in, no phoning home.
- **Production-grade by default.** TLS, SSO and observability are the baseline, not add-ons.

## Status

Early development, built in the open. The platform runs our own dev and prod environments today. Follow along or open an issue.

## Contributing

Contributions are welcome. Read the [contributing guide](https://github.com/QuarantineAl/.github/blob/main/CONTRIBUTING.md) first.

## License

Open source. See each repository for its license.
