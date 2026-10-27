{% raw %}
## 2026-10-19 — Studio-wide Privacy Policy + Terms of Use publish (TSQ-Build)

1. **Date and task:** 19 Oct 2026. Replaced the Sit Tight-only `privacy-policy/` and `terms-of-use/` pages with studio-wide TrueSquare Digital documents covering all games, past, present and future, operated by AP Finish Carpentry LLC. Same URLs. Andrew approved the picks at 7:05 AM ET: Ohio law, Fairfield County courts, no arbitration, 13+, $50 cap, address published, effective date = publish date.
2. **Approach, tool and cost:** Markdown sources were finalized on the box and converted to HTML (python-markdown) inside the existing page template (header, footer and `/styles.css` unchanged; only `<main class="wrap legal">` and the meta descriptions were replaced). Committed to `main` (the Pages source): publish commit b65e2a9, Pages deploy 251d1d6. Rendered with headless Chrome via Playwright at 390x844 DPR 3 and 1440x900. Cost: $0, no third-party uploads.
3. **What worked and how it was verified:** The visible-text grep for `[`, `]`, TODO, NOTE, TBD, draft, PLACEHOLDER, "must match" and `{{` found 0 hits on both pages. The live fetch shows "Effective date: 19 October 2026". scrollWidth equals innerWidth at 390 px, so there is no horizontal scroll.
4. **What failed and why:** The first publish broke the whole GitHub Pages (Jekyll) build. A markdown doc in the repo contained a literal `{{`, and Jekyll's Liquid parser treated it as a template tag, so the deploy failed for every page. It was fixed by wrapping that text in `{% raw %}` … `{% endraw %}`; Pages then deployed 251d1d6 (publish commit b65e2a9) at 7:30 AM ET. Separately, the old live privacy page had shown the internal reminder "This policy must match the Play Data safety form" to the public, because the port from Google Sites copied working notes into page copy.
{% raw %}
5. **Lesson:** Keep legal sources in markdown, with every working note held in a separate NOTES file, and run the internal-note grep on the rendered text before any legal page is committed. Pages deploy from `main`, so a commit there is a publish. On a Jekyll-built Pages repo, any `{{` or `{%` in a .md or .html file (docs included, not just pages) must be wrapped in raw tags, or `.nojekyll` added. Grep for them before pushing and confirm the Pages build is green before fetching the live URLs.
6. **Footer and measure:** Centred the footer social glyphs in their circles and capped the privacy policy and terms text column at 68ch on desktop. Phone layout unchanged.
{% endraw %}

## 2026-10-26 - Privacy policy round 3: score, attempts, Privacy Sandbox (not merged)

1. **Task:** Andrew approved the Amber Fire Data safety addon lines. Add attempt count and score (Amber Fire only) to Section 2(c), reword the Summary and 2(a) lines that said we receive no copy of progress, add one 2(b) line on Android Privacy Sandbox (Topics, Attribution Reporting), set Last updated to 26 October 2026. Keep it true for Sit Tight. Do not merge.
2. **Approach and cost:** Read both games' scripts/Analytics.gd. Amber Fire (cursor/af1-firebase) sends level, mode, attempts, duration, success, reason, and score on level_start, level_end, and level_continue. Sit Tight 1.1.1 (RedBerth cursor/st-firebase-111, 93c9b7b) sends level, mode, attempts, duration, success, and reason, with no score. Edited only four lines in the HTML and added one paragraph. Cost: $0. No third-party uploads.
3. **What worked and how it was verified:** Diff shows only those four lines plus the new 2(b) paragraph. No em or en dashes and no double curly braces in the new text.
4. **What failed and why:** The policy said saves never reach us, but both games already sent attempts, and Amber Fire also sent score, through Firebase. The round 1 policy described event names without checking event params.
5. **Lesson:** When a policy names analytics events, list the params of each game from the code, and say which game sends which. Section 6 was also fixed in this round: no accounts, saves on device, and only the limited analytics in Section 2(c) reaches us.

2026-10-26 - Privacy policy only: Firebase Analytics, 14-month retention, consent mode, impression-level ad revenue, ad rating T, no in-app or ID-based analytics deletion. Children lines that differ (EU minimum age, future mixed audience, prompt deletion) left for Andrew. Not merged. scrollWidth matched innerWidth at 390 and 1440.

## 2026-10-26 - Privacy wording round 2 (not merged)

1. **Task:** On branch cursor/privacy-firebase-analytics-9b4a, apply the Director decisions: replace the EU minimum-age sentence, keep the future child-directed line, restore support-email deletion with the same analytics limit in sections 6, 7, 8, and the parents paragraph, and use the title Amber Fire: Night Match on the policy and the games catalog. Do not merge.
2. **Approach and cost:** Edited the existing HTML only. Terms already used that title, so it was not edited. Headless Chrome measured scrollWidth against innerWidth at 1440 and 390. Cost: $0. No third-party uploads.
3. **What worked and how it was verified:** Privacy and games pages both reported scrollWidth equal to innerWidth at 1440 and at 390. A repo grep for the retired catalog title and the two old age phrases returned no hits. Last updated stayed 25 October 2026.
4. **What failed and why:** No failed approach this round. The terms page needed no edit because the title was already there.
5. **Lesson:** When one deletion rule is decided, copy the same sentences into rights, deletion, retention, and the parents paragraph in the same edit. A title change has to include meta descriptions, not only the visible card heading.

## 2026-10-25 - Privacy policy Firebase/analytics update

1. **Task:** Update the live TrueSquare Digital privacy policy so it covers Firebase Analytics before either game's Firebase build reaches users. Andrew approved. Squash-merged to main as ef399c6 and is live. Same night, Sit Tight Data safety was submitted for com.truesquare.sittight. Amber Fire was not touched.
2. **Approach and cost:** Two rounds on cursor/privacy-firebase-analytics-9b4a, then a squash to main. Round 1 commit 5348d8d added the Firebase section, 14-month retention, consent mode, and a rule that analytics records cannot be deleted for one person. Round 2 commit bddac00 applied the Director decisions: EEA, UK, and Switzerland consent wording, support-email deletion on request, the same analytics limit in sections 6, 7, 8, and the parents paragraph, and the title Amber Fire: Night Match on the policy and the games catalog. Cost: $0. No third-party uploads. Data safety used the Play Developer API for that package, with Andrew's OK at 10:31 PM ET.
3. **What worked and how it was verified:** Headless Chrome showed scrollWidth equal to innerWidth at 1440 and at 390 on the privacy policy and the games catalog. Last updated stayed 25 October 2026. Before the Play call, the live privacy page had 13 Firebase mentions (10:32 PM ET). Data safety attempt 2 at 10:33 PM ET returned HTTP 204. The form says deletion No, crash logs kept, encrypted in transit, no accounts, and approximate location, app interactions, diagnostics, and device or other IDs collected and shared for analytics, advertising, and fraud prevention.
4. **What failed and why:** Review caught leftover deletion promises in sections 6, 8, and 10 after round 1, and a title mismatch (the policy said Amber Fire, the catalog still used the old prototype name, and the terms page already said Amber Fire: Night Match). Root cause: section 7 was rewritten on its own, and the product name was not grepped across the site before review. Data safety attempt 1, also 10:33 PM ET, returned HTTP 400 because the CSV was built from Google's help-page sample. That sample is outdated and omitted the account-creation question the API now requires.
5. **Lesson:** Grep the whole site for every changed promise and product name before review. For Play Data safety, start from that app's own Play Console Export to CSV, not the help-page sample.

## 2026-10-26 - Privacy policy: Firebase Crashlytics (Amber Fire, not merged)

1. **Task:** Founder-approved edit to privacy-policy/index.html for Amber Fire shipping Firebase Crashlytics. Update Section 2(d) heading and copy, remove crash-reporting tools from 2(g), name Crashlytics in Sharing and Retention, keep Last updated 26 October 2026. Open PR to main; do not merge.
2. **Approach and cost:** Edited only privacy-policy/index.html (four spots) and appended this log. Linked Firebase Crashlytics to firebase.google.com/support/privacy to match the existing Firebase Analytics doc link style. Cost: $0. No third-party uploads.
3. **What worked and how it was verified:** git diff limited to privacy-policy/index.html and docs/AGENT_LEARNING.md. Repo script or grep for Liquid open-brace patterns outside raw blocks returned 0 hits. No em or en dashes in new policy text.
4. **What failed and why:** No failed approach this round. Section 2(d) still said platform-only while Amber Fire already used Crashlytics in the build.
5. **Lesson:** When a game adds Crashlytics, update 2(d), Sharing, and Retention in the same pass, and drop future-feature crash-tool wording from 2(g) so the policy does not contradict the ship.

## 2026-10-26 - Studio site Direction A goes live (PR, not merged)

1. **Task:** Andrew approved taking truesquaredigital.com live as the Direction A studio site (dark amber, real TrueSquare Digital logo, official Google Play badge), via the Director. Feature Sit Tight: Slide Car Puzzle (live, Play link) and Amber Fire: Night Match (coming soon, no Play link). Keep every existing URL working. Open one PR, do not merge.
2. **Approach and cost:** Ported the approved box mockup (site-mockup/src/A.html, base.css, A.css) into index.html plus a new studio.css used only by the home page. Swapped the mockup's keyed logo and wordmark for the repo's own assets/truesquare-mark.png with a text wordmark, and kept the repo's google-play-badge.png. Added the mockup's game art (Sit Tight feature graphic and two screens, Amber Fire title, board, Level Clear, wide crop, current icon) under assets/. Kept the /#faq and /#studio anchors that inner pages link to. Inner pages only got the shared header wordmark, Barlow Condensed headings and the amber palette through styles.css; the games page now features Amber Fire with the approved copy. Local render: python http.server plus headless Chrome over CDP, with Google Fonts and YouTube URLs blocked so nothing was fetched from third parties. About 30 min of agent time, no paid credits.
3. **What worked and how it was verified:** 0 broken images and scrollWidth equal to clientWidth at 1280 and 390 on home, privacy policy, games, terms, support and 404. Home has the games, studio, faq and follow anchors. app-ads.txt and CNAME blob hashes are unchanged. The privacy policy body, including the Crashlytics section, is untouched (diff is header and font link only). A grep for double curly braces and brace-percent across the repo shows only the existing raw-wrapped lines in this log.
4. **What failed and why:** The inline GitHub tools cannot commit files, so the branch push has to come from a cloud agent or another authorised git client. The mockup's .coming grid breakpoint (860) did not match styles.css (900), caught in review and fixed.
5. **Lesson:** When porting a mockup into a live site, list every in-site anchor and URL the old pages link to before replacing the home page, and keep each one. Check the target repo's breakpoints instead of copying the mockup's.

## 2026-10-26 - Studio site v2: real logo assets after Eye FAIL (PR #7, not merged)
- Task: Eye failed v1 on 3 assets: live-text wordmark, low-res 112px mark, mid-blast amber still.
- Approach / cost: one follow-up commit; wordmark image tsq-wordmark.png (900x93) in header and footer of every page, tsq-logo-mark.png (251x256) for header, footer, hero and favicon, amber-carpet.jpg re-exported 540x960 from approved still 05_bomb_full_row. Local headless render, about 15 min.
- Worked: images displayed at 2x or denser everywhere (hero 120px from 251px source); 0 broken images and no overflow at 1280 and 390 on all 6 pages.
- Failed: a bulk string replace rewrote the mark src into a bad filename on inner pages and the hero lost its aspect ratio from the new height attribute; both caught by the broken-image and size checks before commit.
- Lesson: ship brand marks as the real image files from the start, never re-typeset a wordmark in a web font, and always set height auto when adding width and height attributes to a sized image.

## Durable (studio site, seeded 2026-10-27)

- Studio Privacy and Terms are shared across all titles. Same URLs. Update before Firebase or Crashlytics ships. Grep each game analytics event params before claiming no progress copy in policy text.
- Founder locks legal picks once (governing law, courts, arbitration, age, liability cap, address, effective date). Do not reopen.
- Jekyll GitHub Pages: any Liquid openers (double curly braces or brace-percent) in markdown must be wrapped in raw tags, or add .nojekyll. Grep before push.
- Site Direction A (founder pick): real logo mark and wordmark from the approved asset pack. Eye judges logo frames after swaps.
- Play badge or Coming soon: switch only with founder OK after the store listing is live.
- Do not commit secrets. No Play JSON, keystores, or google-services.json on the site repo.

## 2026-10-27 Durable seed (Amber Fire exit audit)

1. **Task:** Learning-log audit after Amber Fire 1.0.0 (3) production submit. Site log had dated Privacy and Direction A entries but no Durable block on the PR tree.
2. **Approach / cost:** Exit pass only. No site commit from Director until this PR. Draft Durable from existing entries. Andrew approved exit docs 2026-10-27 7:31 AM America/New_York; next title TBD with him (not assumed).
3. **Worked:** Privacy rounds and Direction A logo fix already recorded.
4. **Failed / why:** Without Durable, the next agent re-reads long PR notes and can re-break Jekyll or policy wording.
5. **Lesson:** Every studio surface that agents edit gets Durable plus a 5-part Log on day one.

