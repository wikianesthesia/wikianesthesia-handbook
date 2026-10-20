# ADR 002 — Public content and the handbook are licensed CC BY-SA 4.0

**Status:** Accepted (2026-10-20, Chris)
**Context:** WikiAnesthesia's mission is *anesthesia knowledge freely accessible
to everyone, everywhere*. The wiki's `WikiAnesthesia:General_disclaimer` page has
long stated that "this work is licensed under a Creative Commons
Attribution-ShareAlike 4.0 International License", yet the platform configuration
declared no license at all (`$wgRightsText`, `$wgRightsUrl`, `$wgRightsPage` empty),
so the site footer, `Special:Version` and the API said nothing — and the same
disclaimer page also carries an older clause describing all content as
WikiAnesthesia's property under a "limited, personal, noncommercial" license,
which contradicts the CC statement. The handbook, now public, needed a license
too.

---

## Decision

1. **Public wiki content is licensed CC BY-SA 4.0** (Creative Commons
   Attribution-ShareAlike 4.0 International), as the disclaimer already states.
2. **Private practice-group content and personal user notes are not covered.**
   They are institutional or personal material held under the platform's privacy
   promise; the license applies to content readable by the public. Wording that
   surfaces the license must not imply otherwise.
3. **The handbook's text is licensed CC BY-SA 4.0** (`LICENSE` in this repository).
4. The platform **declares** the license where MediaWiki surfaces it: the footer
   ("Content is available under … unless otherwise noted"), `Special:Version`, and
   the API's site-info — via `$wgRightsText`, `$wgRightsUrl` and `$wgRightsPage`
   pointing at the disclaimer page.

## Consequences

- `config/LocalSettings-WikiAnesthesia.php` in the web repo sets the three values;
  this rides the next release build (2.0.0 if a rebuild happens before the tag,
  else 2.0.1).
- The disclaimer page's "property of WikiAnesthesia … personal, noncommercial
  use" clause must be reconciled with the CC statement — content work on the wiki,
  tracked in Linear.
- Code repositories are separate: the software license for `wikianesthesia-web`
  and `wikianesthesia-app` (private today) is a later decision; CC BY-SA is a
  content license and is not recommended for code.
