# ADR 001 — Repository topology: three repos, contract-coupled, with an organization handbook

**Status:** Accepted (2026-10-20, Chris + Claude)
**Context:** WikiAnesthesia has two production codebases — the web platform
(`wikianesthesia-web`: MediaWiki extensions and skins, Docker deployment,
infrastructure) and the Flutter mobile app (`wikianesthesia-mobile`, being renamed
`wikianesthesia-app`) — plus organization-level documentation that until now lived
inside the web repository (mission and strategy, organization and outlook, the
access model, the work-tracking agreement). The app depends on the website: it
hardcodes the URL structure, consumes read-only APIs, and scrapes two DOM
couplings. The question was whether that dependency, and the shared documentation,
warrant a monorepo or a meta-repository, and where organization-wide agent
instructions should live so they are maintained once.

---

## Decision

1. **Three separate repositories.** `wikianesthesia-web`, `wikianesthesia-app`,
   `wikianesthesia-handbook`. No monorepo, no meta-repository with submodules.
2. **The app depends on the web platform through a versioned contract, not a build
   link.** The web repo owns the contract document
   (`docs/integrations/mobile-app.md`) and the end-to-end tests that pin it. The
   platform's own SemVer (web ADR 016) governs it: a change that breaks the
   contract is a **major** platform version. The app declares the platform major it
   requires and reads the contract from a tagged web release, never from `main`.
   An app release never requires a website release; a website major is the only
   event that forces app work, and it is run as a Linear project spanning both
   teams.
3. **Organization-level documentation lives in the handbook**, and each code
   repository's `AGENTS.md` cites it by URL. Mission and strategy, organization and
   outlook, strategy and evolution, the production promises as promises, the access
   model summary, the work-tracking agreement, and cross-repo ADRs move here. Each
   code repo's `AGENTS.md` stays short and repo-specific.
4. **The handbook is not a team in Linear.** Its work is an Area label (`handbook`)
   in the `WEB` team and a project when a bounded piece of work exists.

## Rationale

- The two codebases share nothing at the build level: Flutter versus PHP and
  Docker, Codemagic versus GitHub Actions, app-store review cadence versus
  deploy-on-merge. A monorepo makes every tool fight the other half; a
  meta-repository is ceremony a one-maintainer organization stops updating within a
  month.
- The real dependency is one-directional and narrow. Stating it as a contract
  with a version is the standard pattern and costs nothing; wiring it is what the
  monorepo would have bought, and it is not needed.
- Shared agent instructions were previously reached by relative paths into a
  sibling checkout (`../wikianesthesia-web/docs/...`), which breaks for any agent
  that clones one repository alone. One home, cited by URL, is maintained once and
  reachable from anywhere.

## Consequences

- The web repo's `docs/mission-and-strategy.md`, `docs/organization-and-outlook.md`
  and `docs/strategy-and-evolution.md` migrate here; both code repos' `AGENTS.md`
  files link here instead of to each other. The migration is tracked in Linear and
  described in this repo's `.context/SESSION_HANDOFF.md` until done.
- The web repo's `docs/integrations/mobile-app.md` gains a "platform major
  required" statement mirrored in the app's README.
- Nothing about release mechanics changes: each repo releases on its own cadence
  (web: tag + image digest per web ADR 016; app: app-store builds via Codemagic).

## Follow-ups

- Rename `wikianesthesia-mobile` → `wikianesthesia-app` on GitHub before binding
  the Linear `APP` team to it; update Codemagic, local remotes, and the web repo's
  `../wikianesthesia-mobile` references.
- Execute the documentation migration (see the session handoff).
