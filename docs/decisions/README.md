# Decisions — organization-level ADRs

Architecture decision records for choices that span WikiAnesthesia's repositories.
Decisions internal to one codebase live in that codebase's `docs/decisions/`
(the web repo's series runs 001–017 as of 2026-10-20 and is unaffected by this
one).

| # | Decision | Status |
|---|---|---|
| [001](001-repository-topology.md) | Three separate repositories (web, app, handbook); no monorepo, no meta-repo; the app depends on the web platform through a versioned contract; organization docs live in the handbook | Accepted |
