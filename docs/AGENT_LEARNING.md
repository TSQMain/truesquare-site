# Agent learning log (truesquare-site)

New entries: one line each: `YYYY-MM-DD | task | failed because | tried instead | result/lesson`. Older entries: AGENT_LEARNING_ARCHIVE.md. Studio-wide lessons: StudioDrive/studio-brain/lessons.md.

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

## 2026-10-27 - Amber Fire live on Play: site cards switched (PR pending, not merged)
- Task: the daily live-on-Play routine found https://play.google.com/store/apps/details?id=com.truesquare.amberfire&hl=en_US serving the real listing ("Amber Fire: Night Match - Apps on Google Play") on 2026-10-27 at about 9:15 AM ET, so switch the Amber Fire cards to live the same way Sit Tight is shown.
- Approach / cost: branched from origin/main ff5be0c. Home card: "Coming soon" status became "Live on Google Play", the dashed "Coming to Google Play" chip and the Instagram launch-news button became the official badge (assets/google-play-badge.png) linking to the Amber Fire listing with the site's usual UTM tags; meta and og descriptions and the launch FAQ now say it is live. Games page: pill "Available now", badge plus YouTube button like Sit Tight, and an "Amber Fire on Google Play" footer link. The card art (amber-wide.jpg) already carries the current title art, so no icon was needed. Local render with python http.server plus headless Chrome at 1280 and 390. About 10 minutes, no paid credits.
- Worked: both cards match Sit Tight's treatment at desktop and mobile widths with no layout change.
- Failed / held back: the privacy policy also says Amber Fire is "coming soon"; left untouched in this PR because Sit Tight 1.1.2 (RedBerth PR #7) syncs privacy.html from the site and checks it, so a policy edit should be made together with that sync.
- Lesson: check other repos that mirror a page (here the privacy policy) before editing it in a small status PR.

## 2026-10-28 - Media tab (PR, not merged)
- Task: ship the approved Media pages at /media/, /media/sit-tight/, and /media/amber-fire/. Four Sit Tight mp4s stay at those exact URLs. Nav on editable pages is Games, Media, Studio, FAQ, Support. Footer links are Games, Media, Studio (/#studio), FAQ (/#faq), Privacy, Support. Home and Games titles become Sit Tight: Car Parking Jam and Amber Fire: Night Bubble Match.
- Approach / cost: layered the Eye-passed media.css on the live studio.css and reused that header and footer. Dropped the red mock banner and noindex. Copied the mp4s, posters, media-tile-sittight.jpg, amber-combo.jpg, and sittight-icon.png byte for byte from the mock tarball. Did not edit privacy-policy, terms, app-ads.txt, or CNAME. Cost: $0. No third-party uploads.
- Worked: python http.server. All four clips answered video/mp4. Headless Chrome showed scrollWidth equal to clientWidth at 390 and 1440 on home, games, the three media pages, support, privacy, terms, and 404. No broken local images or links. Page load requested 0 mp4 files. Tap on clip 1 played it in place; tap on clip 2 paused clip 1.
- Failed / held back: a first overflow check flagged the "More games soon" pill at 390. Its box sits past the viewport inside the horizontal pill scroller, and page scrollWidth stayed 390, so it is the approved peek. The brief named two new jpgs; the pills also need sittight-icon.png, which was not already in the repo. Privacy and terms still have the old nav, footer, and game names, because this task said not to touch those pages.
- Lesson: reuse studio.css and add only a page stylesheet. Copy published mp4s byte for byte and never rename them. Measure page scrollWidth apart from children inside an overflow scroller. Leave the privacy policy out of a media PR, since the game repo syncs that file.

## 2026-10-28 - Amber Fire clips and Privacy/Terms nav (PR, not merged)
- Task: serve four Amber Fire mp4s at /media/amber-fire/ with the given filenames, byte for byte, show them like Sit Tight, and switch the Privacy and Terms header to Games, Media, Studio, FAQ, Support. Do not change policy text, Sit Tight media files, or the studio logo. Do not merge.
- Approach / cost: copied the four uploads and checked sha256. Posters are 540x960 jpeg frames, same size as the Sit Tight posters. Header nav only on the two legal pages. Cost: $0. No third-party uploads.
- Worked: python http.server. Served bytes matched the four sha256 values and video/mp4. Headless Chrome at 1440 and 390: scrollWidth equaled clientWidth, 0 broken images, 0 mp4 requests on load, on home, games, media, both game media pages, privacy, terms, support, and 404. A real click played Earthquake, then Bomb rows paused it. A desktop walkthrough showed the same and the new header on Privacy and Terms.
- Held back: Home and Games title jpgs still say Slide Car Puzzle and Night Match. They are flat rasters, so they were not redrawn. The policy body still uses the old titles because this task said not to change policy text.
- Lesson: hash the mp4 after it is in the repo path, and add only a poster beside it. A title baked into a jpg stays until there is new art.
2026-10-28 - Instagram Reels via Buffer reject >60fps-reported clips; keep 30fps _ig30 copies.
2026-11-02 - Link-in-bio /yt/, /tt/, and /ig/ reuse the studio header, footer, studio.css, and the media game row. Play links use a referrer (youtube, tiktok, or instagram with social, and website with web, campaign tsq_organic). Local render: no broken images, scrollWidth matched clientWidth at 1280 and 390.

## 2026-11-17 - Full maintenance pass (web)

1. **Task:** Audit all pages, links, Play links, app-ads.txt, privacy, sitemap, robots, meta and Open Graph; draft a Shatterwave coming-soon card; triage PRs #11 and #8. Nothing merged.
2. **Approach and cost:** Scripted link and meta crawl of every HTML file, curl status check of the live site, live Play page title check. Cost: $0.
3. **Result:** 0 broken internal links, 0 broken Play links, every page 200, app-ads.txt exact. Fixed: em dashes in five page titles, and stale game names on Privacy and Terms (Slide Car Puzzle, Night Match) that did not match the live Play titles.
4. **Open:** Privacy text for Shatterwave still says no in-app purchases and ads off in the first release. The Play SKU shatterwave_remove_forced_ads is active, so ads-analytics and the founder must confirm before launch.
5. **Lesson:** Compare site and legal game names against the live Play title, not an earlier Director decision.

## 2026-11-17 - Shatterwave privacy draft (web, PR draft, not merged)
1. **Task:** Fix every Shatterwave gap in the privacy policy from the ads-analytics fact sheet (ads on, purchase, AD_ID and permissions, Remote Config and Play update/review, analytics timing, IP-derived location, share sheet). Founder approves before merge.
2. **Approach and cost:** Edited only privacy-policy/index.html, using the fact sheet's file:line evidence. Terms of use had no Shatterwave-specific claims, so it was left alone. Cost: $0.
3. **Result:** Date set to 17 November 2026. Sit Tight and Amber Fire text untouched except the shared score sentence, which now names Shatterwave.
4. **Open:** Sit Tight (RedBerth) mirrors this file, so the sync check must be rerun if this merges. The "coming soon" status wording for Shatterwave is unchanged until launch. Items in the fact sheet's "Could not verify" list remain open.
5. **Lesson:** Describe analytics timing by actual behavior and point to "consent signals where required", so a later Consent Mode change does not make the policy wrong.

## 2026-11-19 - Shatterwave launch prep (web, draft PR, not merged)
1. **Task:** Prep the site for Shatterwave's public release: game page, home and games cards, sitemap, privacy and app-ads check.
2. **Approach and cost:** No per-game pages existed, so /games/shatterwave/ reuses the games-index card (game-feature) plus a screens row, with the same header and footer. Screens are resized real captures from the game repo docs/captures. Cost: $0.
3. **Result:** Privacy already covered AdMob with UMP, Firebase Analytics, Crashlytics, Remote Config and Play Billing (PR #26). Only gap: "coming soon" status on the title list, fixed in a separate commit. app-ads.txt already has pub-5155911610089674, unchanged. All changed pages and assets return 200 locally.
4. **Open:** Merge only when the Play listing is public. Screens are early captures, to be replaced with release-build ones. Boss plurality in captures is unconfirmed, so copy never states a number of bosses.
5. **Lesson:** Headless Chrome will not render below about 500 px wide, so a 390 px screenshot looks cropped. Shoot at 500 for a mobile check.
2026-11-19 | Shatterwave site launch copy (PR #28) | copy still said level is the song / timed boss and used early screenshots | matched page to final 0.1.8 listing, swapped in 4 store shots (resized to 540x960 jpg) | page ready, merge only when Play page is live
2026-11-20 | Per-game media page for Shatterwave (7 b2 teasers) | no media/shatterwave page existed, clips unlisted | built it from the amber-fire page, posters from frame at 1s, added pill and tile on other media pages | PR open, older clip_01..11 and promo left unlisted (no captions given)
2026-11-20 | Media pages: full per-game clip lists | wide promo would crop in 9:16 frame | added .clip.wide (16:9, spans 2) and posters from frame | PR #31 updated; _B and v3 pairs treated as duplicates, kept v3
