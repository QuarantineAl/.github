<p align="center">
  <img src="https://raw.githubusercontent.com/QuarantineAl/.github/main/profile/logo.svg" alt="quarantine" width="120" />
</p>

<h1 align="center">quarantine</h1>

<p align="center">
  <strong>Self-hosted infrastructure that gets out of your way.</strong><br/>
  An open-source, batteries-included platform for running your own services — from zero to production in three commands.
</p>

<p align="center">
  <a href="https://quarantine.al">Website</a> ·
  <a href="https://github.com/QuarantineAl/platform">Get Started</a> ·
  <a href="https://github.com/QuarantineAl/platform/blob/main/CONTRIBUTING.md">Contributing</a>
</p>

---

## Quickstart

```bash
git clone https://github.com/QuarantineAl/platform.git
cd platform
./quarantine init
```

That's it. Answer a few prompts and you have a reverse proxy, SSO, observability, and GitOps deployments running on your own hardware.

## What's inside

| Layer | Tool | Why |
|---|---|---|
| Orchestration | **Docker Compose v2** | Simple, portable, no cluster overhead |
| Reverse proxy | **Traefik v3** | Automatic TLS, label-based routing |
| Identity & SSO | **Zitadel** | Single sign-on for every service |
| Database | **PostgreSQL** (shared) | One instance, many databases |
| Observability | **SigNoz** + OpenTelemetry | Traces, metrics, and logs in one place |
| Deployments | **Komodo** | GitOps-style continuous delivery |
| Secrets | **SOPS + age** | Encrypted secrets, committed safely |

## Philosophy

- **Three commands, not thirty.** Onboarding should be measured in minutes.
- **Convention over configuration.** Sensible defaults everywhere; override only when you need to.
- **Your hardware, your data.** No vendor lock-in, no phoning home.
- **Production-grade by default.** TLS, SSO, and observability aren't add-ons — they're the baseline.

## Status

🚧 **Early development.** The core stack is defined and the foundation is being built in the open. Follow along, open issues, or jump into discussions.

## Contributing

Contributions are welcome — check the [contributing guide](https://github.com/QuarantineAl/.github/blob/main/CONTRIBUTING.md) and open issues labeled `good first issue`.

## License

Open source. See individual repositories for license details.