# ADR 003 — Installed app versions keep working against the website

**Status:** Accepted (2026-10-28, Chris)
**Context:** The mobile app depends on the website through a versioned contract (ADR 001). The contract covers:
- the URL structure;
- the read APIs;
- the session check;
- two DOM couplings.

Its document is the web repository's `docs/integrations/mobile-app.md`.

ADR 001 settles what happens when that contract breaks: a major platform version (web ADR 016), run as a Linear project across both teams. It doesn't say *for how long* the old contract must keep working, and that is where an app differs from a website:
- a store release can't be recalled from the phones that installed it;
- people update late, or not at all;
- store review delays even an urgent fix.

The app's own release workflow (app repository `docs/decisions/002-branches-merges-releases.md`) surfaced the question.

---

## Decision

1. **App versions still in use keep working.** When the website changes something the app depends on:
   1. The new behavior ships **alongside** the old.
   2. An app release that uses the new behavior follows, tested against the website before and after the switch.
   3. The old behavior is retired only after the support window.
2. **The support window is a guideline: six months** after the first app release that no longer needs the old behavior. Analytics show which app versions are still in use.

   It is not a strict requirement. The app is new, barely announced, and has a small user base. The maintainers may shorten or lengthen the window for a given change; the reason is recorded in that change's Linear project.
3. **A breaking change is still a major platform version,** and still a cross-team project (ADR 001, web ADR 016). This decision adds only the timing.
4. **A minimum-version check in the app,** if one is ever added, can't protect versions that shipped without it. It must never lock users out of the app's offline clinical tools because a website feature changed.
5. **The app's production touchpoints are a person's acts.** In the access model, these count as touching production for the app:
   - uploading a build to App Store Connect or the Play Console;
   - submitting it for review;
   - releasing it;
   - tagging a release.

   Agents prepare and check them; a maintainer performs them.

## Rationale

- **A website can be rolled back, and an installed app can't.** The only way to keep old app versions working is to keep serving what they expect.
- **Six months** covers people who update rarely, without making the website carry old behavior indefinitely.
- **A guideline, not a rule:** with today's small user base, a rigid window would cost more than it protects. The record of each deviation keeps the choice deliberate.
- **Production touchpoints:** ADR 001's access model already says agents don't publish to the app stores. Naming each store step removes doubt about uploads and tags, which don't look like "publishing" but can't be undone.

## Consequences

- **The web repository's `docs/integrations/mobile-app.md`** states the window when it next changes. A contract change's Linear project includes the dates the old behavior ships alongside, and when it retires.
- **The app repository's runbook** (`docs/runbooks/release.md`) checks every release against the contract, and follows this decision when the contract is changing.
