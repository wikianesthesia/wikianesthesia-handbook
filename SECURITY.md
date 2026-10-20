# Security policy

WikiAnesthesia runs live clinical software: a public anesthesia reference that
also holds private institutional content, and a mobile app that computes drug
doses. We take reports seriously and we would rather hear about a problem
privately than read about it publicly.

## Reporting a vulnerability

- **Email:** admin@wikianesthesia.org — include what you found, how to reproduce
  it, and what you believe the impact is. Encrypting the report is welcome but
  not required; please do not include real patient or user data.
- **GitHub:** the code repositories accept private vulnerability reports through
  GitHub's *Report a vulnerability* button where it is enabled.

Please **do not** open a public issue for a security problem, and please do not
test against practice-group (institutional) content you are not a member of: that
content is real and private.

## What to expect

A volunteer team runs this organization. We aim to acknowledge a report within a
week and to tell you what we found and what we intend to do. We will credit you in
the fix's record if you wish.

## Scope

- `wikianesthesia-web` — the MediaWiki platform at wikianesthesia.org and its
  deployment.
- `wikianesthesia-app` — the mobile app (formerly `wikianesthesia-mobile`).
- The production site itself, wikianesthesia.org.

Out of scope: third-party services we merely use (MediaWiki core and upstream
extensions — report those upstream; AWS; app stores), and denial-of-service
testing against the live site.
