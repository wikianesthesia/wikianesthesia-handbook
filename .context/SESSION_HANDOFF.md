# Session handoff — the handbook

The tracked relay between work sessions on this repository. Rewrite it at the end
of any material session and commit it, so the next session resumes from the
repository alone.

## Snapshot

- Date: 2026-10-20
- State: **skeleton only.** Created in a `wikianesthesia-web` session that had the
  full context of why this repo exists (see ADR 001). No organization documents
  have moved yet. Remote: `github.com/wikianesthesia/wikianesthesia-handbook`
  (private for now — see the visibility note below).

## Exact next action — the migration (a fresh session rooted here)

Decide visibility first (maintainer): the handbook is designed to hold no
secrets (the web repo's gitignored `docs/private/` never moves here), so it can
be **public** — which lets agents in any repo read it by raw URL with no local
clone and no freshness problem. If it stays private, every code repo's `AGENTS.md`
instead instructs agents to keep a sibling clone current
(`git -C ../wikianesthesia-handbook pull --ff-only`, cloning if absent).
Then, in one session with both sibling checkouts present
(`../wikianesthesia-web`, `../wikianesthesia-app`):

1. **Move the organization documents** from the web repo into `docs/` here with
   `git mv`-equivalent history notes: `docs/mission-and-strategy.md`,
   `docs/organization-and-outlook.md`, `docs/strategy-and-evolution.md`. Rewrite
   their internal relative links. Leave a one-line pointer file behind in the web
   repo only where the web docs gate (`scripts/check-docs.py`) would otherwise
   report a dangling reference — then fix the references instead and delete the
   pointer.
2. **Rewrite references in the web repo**: `AGENTS.md` (§ Document map's "org-level
   set" bullet → handbook URLs; mind the 16 KiB budget), `README.md`, `ROADMAP.md`,
   `ARCHITECTURE.md`, `docs/README.md`-style indexes, `extensions/PracticeGroups/PRIVACY.md`
   and `extensions/UserNotes/PRIVACY.md` (they cite the mission doc), and any
   `docs/decisions/*.md` that link the three files. `grep -rn 'mission-and-strategy\|organization-and-outlook\|strategy-and-evolution'`
   across the repo is the checklist. Run `python3 scripts/check-docs.py` → `OK`.
3. **Rewrite references in the app repo**: its `AGENTS.md` cites
   `../wikianesthesia-web/docs/mission-and-strategy.md` and
   `../wikianesthesia-web/docs/organization-and-outlook.md` by relative path —
   replace with handbook URLs, and add a one-line "requires platform major 2;
   contract: web repo `docs/integrations/mobile-app.md` at the matching tag"
   statement to its README (ADR 001 §Consequences).
4. **Both code repos' `AGENTS.md`** gain a one-line pointer near the top:
   "Organization-level context: https://github.com/wikianesthesia/wikianesthesia-handbook/blob/main/AGENTS.md".
5. Add a minimal docs gate here (dangling-link check; the web repo's
   `scripts/check-docs.py` is the model, trimmed), and a GitHub Actions workflow
   that runs it.
6. Linear: the migration is issue `WEB-…` (label `handbook`, project "Handbook
   migration" if it grows past one issue). Close it with the commit hashes from
   all three repos.

## The sweep — what belongs here, from both code repos (do with the migration)

The test: *is it true for the organization regardless of codebase?* If yes it
lives here and the code repos link to it; if it is about one codebase it stays
there. Each fact in exactly one place.

**Moves here (after a sensitivity review — this repo is PUBLIC; the web repo was
private):** `docs/mission-and-strategy.md`, `docs/organization-and-outlook.md`
(names people and institutions — confirm with each person what may be public, or
generalize), `docs/strategy-and-evolution.md`.

**Becomes a living page here, summarized from a web ADR that stays as the
record:** `docs/work-tracking.md` (the Linear operating guide: teams WEB/APP/
CONTENT, label axes, flags, triage, views, how agents use it — from web ADR 017
and the 2026-10-20 setup); the production promises (from web ADR 014, the
PRIVACY.md contracts, `docs/integrations/mobile-app.md`, the app's physician
sign-off rule) — already summarized in `AGENTS.md` here.

**Shrinks in the code repos to a link + the repo-specific remainder:** web
`AGENTS.md` §"What this project is" (org paragraph) and the org-wide half of
§"Hard constraints" (no production SSH ever; secrets never committed); app
`AGENTS.md` §"What this project is" (org context, mission, the
"seed of technical redundancy" note) and the org-wide half of its constraints.
The web `AGENTS.md` byte budget (16 KiB) makes this shrink welcome.

**Stays where it is:** web `docs/aws.md`, `docs/integrations/mobile-app.md` (the
web repo owns the contract), ADRs 011/013/016/017 (records), all runbooks,
`docs/issues/`; app `issues/`, `docs/reviews/`, clinical gotchas; both `CLAUDE.md`
shims.

**Gaps found while surveying (open as Linear issues):** the wiki content has no
declared license (`$wgRightsText` is empty in the tracked config) — an
organization decision (CC BY-SA 4.0 is the wiki-world norm; mission says "freely
accessible") that then lands in the web config; neither code repository has a
LICENSE file; the code repositories should enable GitHub private vulnerability
reporting to match `SECURITY.md` here.

## Not in scope of the migration

- Moving ADRs out of the web repo's numbered series (they stay; this repo's
  series is separate and starts at 001).
- Any change to release mechanics or the Linear structure (already ruled: web ADR
  016, web ADR 017 + amendment).
