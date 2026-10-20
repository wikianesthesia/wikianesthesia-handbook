# WikiAnesthesia Handbook

The organization-level home for everything that is true across all of
WikiAnesthesia's repositories and initiatives: the mission and strategy, the
production promises that every codebase must keep, how the repositories relate,
how work is tracked, and how releases happen. If a fact belongs to one codebase
it lives in that codebase; if it belongs to the organization it lives here.

**WikiAnesthesia** is a 501(c)(3) nonprofit whose mission is *anesthesia
knowledge freely accessible to everyone, everywhere*: a collaborative anesthesia
reference ([wikianesthesia.org](https://wikianesthesia.org/), a customized
MediaWiki) with a companion mobile app, built and run by a very small volunteer
team.

## The repositories

| Repository | What it is | Agent orientation |
|---|---|---|
| [`wikianesthesia-web`](https://github.com/wikianesthesia/wikianesthesia-web) | The web platform: custom MediaWiki extensions and skins, the Docker deployment, infrastructure docs, runbooks | its `AGENTS.md` |
| [`wikianesthesia-app`](https://github.com/wikianesthesia/wikianesthesia-app) *(renamed from `-mobile`)* | The Flutter mobile app: native clinical tooling plus a thin integration with the wiki | its `AGENTS.md` |
| **`wikianesthesia-handbook`** (this repo) | Organization docs: mission, strategy, promises, working agreements, decisions that span repos | `AGENTS.md` here |

The repositories are deliberately separate (no monorepo, no meta-repo): see
[ADR 001](docs/decisions/001-repository-topology.md). The one dependency between
them, the app consuming the website's integration contract, is a documented
contract versioned by the platform's SemVer, not a build-time link.

## Contents

- `AGENTS.md` — organization-level orientation for any agent or human working in
  **any** WikiAnesthesia repository; each repo's own `AGENTS.md` layers its
  specifics on top.
- `docs/decisions/` — organization-level architecture decision records (repository
  topology, work tracking, release policy as it spans repos). Index in its `README.md`.
- `docs/` *(migrating in — see the session handoff)* — mission and strategy,
  organization and outlook, strategy and evolution; today these still live in the
  web repository under `docs/`.
- `.context/SESSION_HANDOFF.md` — the cross-session relay: what state the handbook
  is in and the exact next action.

## Work tracking

All work, across every repository and initiative, is tracked in
[Linear](https://linear.app/wikianesthesia): teams `WEB`, `APP` and `CONTENT`,
projects for bounded undertakings, initiatives as the roadmap layer. The web
repository's ADR 017 is the ruling; this handbook carries the working agreement
once the migration lands.
