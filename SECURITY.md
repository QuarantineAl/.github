# Security policy

## Reporting a vulnerability

Please **do not** open a public issue, pull request or discussion for a security problem.

Report it privately through GitHub instead:

1. Open the affected repository, for example [platform](https://github.com/QuarantineAl/platform).
2. Go to the **Security** tab and click **Report a vulnerability**.
3. Describe the problem, how to reproduce it, and what an attacker could do with it.

Only the maintainers can see your report. We'll reply there, keep you updated while we work on a fix, and credit you in the published advisory unless you'd rather stay anonymous.

If you're not sure which repository the problem belongs to, report it on [platform](https://github.com/QuarantineAl/platform/security/advisories/new).

## Supported versions

quarantine is in early development and has no tagged releases yet. Fixes go to `main`; run `quarantine upgrade` to pick them up.

## Scope

Things we especially want to hear about:

- Ways around sign-in (Zitadel, oauth2-proxy) to reach an app or the admin UIs
- Secrets that end up unencrypted, in logs, or in images
- One environment, tenant or PR sandbox being able to reach another's data
- Anything that lets untrusted code run on the self-hosted CI runners
