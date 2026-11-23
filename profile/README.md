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
| Identity & SSO | **Zitadel** | Single sign-on for every service |
| Database | **PostgreSQL** (shared) | One instance, many databases |
| Observability | **SigNoz** + OpenTelemetry | Traces, metrics and logs in one place |
| Deployments | **Komodo** | GitOps-style continuous delivery |
| Secrets | **SOPS + age** | Encrypted secrets, committed safely |

## Built on quarantine

| Product | What it does |
|---|---|
| **Lazzaretto** | Runs coding agents and LLMs from a browser, each session sealed in its own workspace |
| **Kujtime** | A city-by-city memory archive, reviewed by an editorial team and published to each city's channels |
| **BEM** and **delivery-note-ai** | Read warehouse receipts and delivery notes from PDFs and photos into structured data |
| **Interactive Real Estate** | Interactive building and unit explorer for property sites |
| **toolkit** | Shared design system: `@quarantineal/ui`, `icons`, `design-tokens` |

## Principles

- **Three commands, not thirty.** Onboarding is measured in minutes.
- **Convention over configuration.** Sensible defaults everywhere; override only when you need to.
- **Your hardware, your data.** No vendor lock-in, no phoning home.
- **Production-grade by default.** TLS, SSO and observability are the baseline, not add-ons.

## Status

Early development, built in the open. Follow along, open issues, or start a discussion.

## Contributing

Contributions are welcome. Read the [contributing guide](https://github.com/QuarantineAl/.github/blob/main/CONTRIBUTING.md) and look for issues labeled `good first issue`.

## License

Open source. See each repository for its license.
