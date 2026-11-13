# ADR 004 — Every change reaches `main` through a pull request the other maintainer can review

**Status:** proposed 2026-11-13 by Chris; accepted when Jeffrey approves the pull request that adds it.
**Context:** WikiAnesthesia has two maintainers, Chris and Jeffrey, and four repositories: `wikianesthesia-web`, `wikianesthesia-app`, `wikianesthesia-ops` and this handbook. The organization's posture is persistence: the platform must be operable by a successor from the repositories alone. That needs more than documents. Whoever may take over the technical work has to have seen it change, as it changed.

`CONTRIBUTING.md` has always said "short-lived branches, pull requests into `main`", but only the app works that way. Its ADR 002 settled branches, merges and reviews there, and the two maintainers have reviewed each other's pull requests since. Most changes to the web repository, nearly all authored by agents on Chris's account, went straight to `main`, and ops had no rule. Each maintainer saw the other's codebase change only through Linear's summaries.

GitHub can't enforce any of this yet. The organization is on GitHub's Free plan, which offers no branch protection or rulesets for private repositories (web, app, ops). The Team plan, free for verified nonprofits, does (web WEB-114).

---

## Decision

**Branches and pull requests.**
- Trunk-based: `main` is always releasable. Work happens on short-lived branches, and every change reaches `main` through a pull request. No long-lived or per-environment branches; a repository's own ADR may add a short-lived release branch (the app's `release/X.Y`).
- One pull request per piece of work, usually one Linear issue, not one per commit.
- A repository may declare files that go straight to `main` because they are bookkeeping, not changes to what it does. Each declares them in its `AGENTS.md`. The agents' session relay, `.context/SESSION_HANDOFF.md`, is the one such file today.

**Reviews.**
- **The other maintainer reviews,** as a rule.
- **A review need not be line by line.** A maintainer outside a codebase's specialty reviews what the change does, why, and what could go wrong. The description is written for that reader: what changes for users or operators, the risk, and how it was verified, with result lines.
- **Either maintainer may merge their own pull request without review** when they judge it appropriate, an incident on production for one. They first write "Merging without review: <reason>" in it.
- **CI passes before merge,** either way, and clinical values keep their clinician's sign-off (`CONTRIBUTING.md`).

**Merges.**
- **Merge commits only;** never squash or rebase, never force-push. One pull request is still one revert: `git revert -m 1 <merge>`.
- Stacked pull requests merge bottom-up. After each merge, check the next one's base and remaining diff, and let CI run again.

**Agents.**
- Agents branch, commit, push their branch, open the pull request and request the other maintainer's review.
- **An agent never merges or approves a pull request without a maintainer's go-ahead for that pull request,** and never pushes to `main` except the declared bookkeeping files.

**Enforcement.** By convention and by each repository's agent instructions while the organization is on the Free plan. On the Team plan, each `main` requires a pull request, one approving review and passing CI, with both maintainers able to bypass for a recorded self-merge.

## Rationale

- **Visibility is the point.** A pull request shows what changed and why, in order, to the person who may one day own it. A Linear status update summarizes; it doesn't show the change.
- **A second person sees every production-bound change** before it ships, even when the review is about intent rather than code.
- **The app's practice works:** 58 pull requests through October 2026, with stacked reviews, no force-pushes and a recorded way to self-merge.
- **Merge commits** keep stacked pull requests intact without rewriting anyone's branch, which the never-rebase, never-force-push rule needs anyway.

## Alternatives considered

- **Direct pushes, with Linear status updates for visibility:** what web did. Summaries lag and omit, and the other maintainer never sees the change itself.
- **Required review with no self-merge:** an incident would wait for the other maintainer's time zone. The stated reason keeps the exception visible instead.
- **Squash merges and a linear history:** rejected in the app's ADR 002; they break stacked pull requests and force force-pushes.

## Consequences

- **Each repository's agent instructions** require a pull request for every change and name their bookkeeping exceptions: web's `agent/workflow.md` and `AGENTS.md`, the app's `AGENTS.md`, ops' `AGENTS.md`, and this handbook's `AGENTS.md`.
- **The app's ADR 002** keeps its app-specific rules (the pull-request template's checks, releases, signing) and defers to this record for branches, merges and reviews, which it already matched.
- **Web** gains a pull-request template written for a reviewer outside the codebase. Its release tooling is unaffected: a deploy ships only what `origin/main` holds and requires that commit's `tests` run to have passed.
- **The maintainers' repository settings:** merge commits only, with merged branches deleted automatically, in web, ops and the handbook, as in the app. Agents don't change repository settings.
- **WEB-114** (GitHub for Nonprofits) turns this record's enforcement on. The handbook is public, so its `main` can be protected now.
