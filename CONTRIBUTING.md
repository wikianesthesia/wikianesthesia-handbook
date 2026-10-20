# Contributing

WikiAnesthesia is built and run by a very small volunteer team, and our bar is
set by what the software does: it is used in clinical settings. These are the
rules that apply across every repository; each repository's `AGENTS.md` and
`README.md` add the specifics.

- **Work is tracked in Linear**, not in GitHub issues (see `AGENTS.md` §How work
  is tracked). A pull request or commit that says `Fixes WEB-54` moves the issue.
  If you are not a workspace member, open a GitHub issue and we will mirror it.
- **Trunk-based.** Short-lived branches, pull requests into `main`, CI green before
  merge. No long-lived or per-environment branches.
- **Clinical values need a clinician.** No dose, hold time, timer interval or
  equipment size enters or changes without physician sign-off against a cited
  source — in either codebase.
- **Privacy is non-negotiable.** Anything that touches practice-group or user-note
  visibility must add a matching guard and a regression test, and gets a written
  analysis in that repository's `docs/issues/`.
- **Evidence over assertion.** A change is done when the verifying command and its
  output say so. Say what you ran.
- **Decisions that others must not reverse unknowingly** are recorded as ADRs: in
  the repository they concern, or here when they span repositories.
- **Agents are contributors too** and follow the same rules. They work on test
  environments only and never touch production; production touchpoints are the
  maintainer's.

Documentation in this repository is written as if it had always been true: no
"previously", no change-date annotations in descriptive text. Chronology lives in
ADRs and git history.
