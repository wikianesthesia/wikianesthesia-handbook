# AGENTS.md — the WikiAnesthesia organization, for any agent in any repo

Organization-level orientation. Every WikiAnesthesia repository's own `AGENTS.md`
assumes you have read this and adds only what is specific to that codebase.
General engineering-workflow conventions come from the contributor's environment;
this file holds what is true about the *organization*.

## What WikiAnesthesia is

A 501(c)(3) nonprofit: *anesthesia knowledge freely accessible to everyone,
everywhere*. Two production surfaces, both live clinical software:

- **The web platform** (`wikianesthesia-web`): a customized MediaWiki at
  wikianesthesia.org — a public reference plus a three-tier knowledge model
  (public / institutional practice groups / personal notes).
- **The mobile app** (`wikianesthesia-app`): a Flutter companion with native
  clinical tooling (ACLS timers, dosing, anticoagulation guidance) that also wraps
  the wiki. It computes drug doses; its stakes are patient safety.

A very small volunteer team runs both. The strategic posture is **persistence,
not growth**: the platform must survive its founders and be operable by a
successor from the repositories alone. Decisions that reverse this are the ones a
newcomer must not make unknowingly; they are recorded as ADRs.

## The promises every codebase must keep

1. **The practice-group privacy boundary.** Practice groups hold real private
   clinical content from named institutions. Title visibility equals content
   readability, per article; private content must never leak through any surface,
   on any repository. The normative contracts are the web repo's
   `extensions/PracticeGroups/PRIVACY.md` and `extensions/UserNotes/PRIVACY.md`.
   The app's institution awareness sits on top of this boundary and is authorized
   by the server, never gated client-side alone.
2. **The external clinical embed.** The web platform serves a chrome-free view
   inside an external clinical system's iframe. Its URL contract and
   iframe-embeddability are production acceptance criteria.
3. **The mobile app's integration contract.** The app hardcodes the website's URL
   structure and consumes read-only APIs and two DOM couplings. The contract is
   `docs/integrations/mobile-app.md` in the web repo; breaking it is a **major**
   platform version (ADR 016 there), never a silent change.
4. **Clinical values need a clinician.** No dose, hold time, timer interval or
   equipment size enters or changes in either codebase without physician sign-off
   against a cited source.

## How the repositories relate

Three repositories, deliberately separate ([ADR 001](docs/decisions/001-repository-topology.md)):
web, app, handbook. Code flows within a repo (trunk-based, tag + image/build
releases); data flows only from production to test environments; the app depends
on the web platform through a versioned contract, not a build link. Cross-repo
work is a Linear project spanning both teams.

## Access model (summary)

Agents never touch production directly: no production SSH, no out-of-fence cloud
writes, no app-store publishing. They work on the expendable **alpha**
environment and the dev stacks, author changes and exact commands, and the
maintainer executes production touchpoints. Secrets never enter any repository.
The full model is the web repo's ADR 011 and ADR 013.

## How work is tracked

Linear (workspace `wikianesthesia`) owns work tracking across all repositories and
non-software initiatives: teams **`WEB`**, **`APP`**, **`CONTENT`**; projects for
bounded undertakings; initiatives as the roadmap layer; labels on two axes (type,
area) plus `maintainer-action`, `agent-ready`, `blocks-cutover`; no cycles;
triage on. A PR or commit that says `Fixes WEB-54` moves the issue. Each code
repo keeps its deep engineering write-ups (security/privacy analyses, ADRs,
specs) next to the code; Linear carries status and discussion. Ruling: the web
repo's ADR 017.

## Working in this repository

The handbook is documentation only. Write every page as if it had always been
true (no "previously", no change-date annotations in descriptive text; chronology
belongs in ADRs and git history). Each fact lives in exactly one place: if it is
about one codebase, it belongs in that codebase, not here. Record decisions that
span repositories as ADRs in `docs/decisions/` and index them in its `README.md`.
Rewrite `.context/SESSION_HANDOFF.md` at the end of any material session.
