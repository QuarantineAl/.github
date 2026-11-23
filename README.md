# QuarantineAl/.github

Org-wide files for [QuarantineAl](https://github.com/QuarantineAl):

- `profile/` holds the org profile page people see on github.com/QuarantineAl.
- `CONTRIBUTING.md` is the default contributing guide for every repo that doesn't have its own.
- `.github/workflows/` holds the reusable workflows that app repos call to deploy onto the [platform](https://github.com/QuarantineAl/platform).

## Reusable workflows

All three run on the org's self-hosted runners. Each environment has its own pool: `[self-hosted, quarantine-dev]` and `[self-hosted, quarantine-prod]`. They work against the platform checkout at `/opt/quarantine/repo` on the runner's host, so the app must already have an entry in platform's `catalog.yaml`. Never call them for untrusted or fork-PR code.

| Workflow | When to call it | What it does |
|---|---|---|
| [`deploy-app.yml`](.github/workflows/deploy-app.yml) | After a merge to a deploy branch | Builds the app's images, pushes them to GHCR tagged with the environment and the commit SHA, and brings the app up pinned to that SHA. Optionally rolls per-tenant instances (`upgrade_tenants`) and publishes a CalVer release on the calling repo (`create_release`). |
| [`pr-sandbox-up.yml`](.github/workflows/pr-sandbox-up.yml) | On PR opened, synchronize or reopened | Builds a `pr-<n>` image and starts an isolated sandbox at `pr-<n>-<app>`. For OIDC apps it also starts that sandbox's oauth2-proxy and registers its redirect URI in Zitadel. |
| [`pr-sandbox-down.yml`](.github/workflows/pr-sandbox-down.yml) | On PR closed | Removes the sandbox and its volumes, then deregisters its redirect URI. |

The caller decides the environment. A typical setup sends PRs against `develop` to dev and PRs against `main` to prod:

```yaml
jobs:
  sandbox:
    uses: QuarantineAl/.github/.github/workflows/pr-sandbox-up.yml@main
    with:
      app: lazzaretto
      environment: ${{ github.event.pull_request.base.ref == 'develop' && 'dev' || 'prod' }}
      pr_number: ${{ github.event.pull_request.number }}
      ref: ${{ github.event.pull_request.head.sha }}
    secrets: inherit
```

`deploy-app.yml` assumes a two-image app (backend + frontend), which is lazzaretto's shape. Lazzaretto is the only caller today. Other apps deploy with their own inline jobs on the same runner pool.

See platform's [`docs/runners-and-sandboxing.md`](https://github.com/QuarantineAl/platform/blob/main/docs/runners-and-sandboxing.md) for the full runner and sandbox model.

## Changing a workflow

Callers pin `@main`, so a merge here takes effect on every caller's next run. Test a change by pointing one caller at your branch (`@your-branch`) first.
