# TrueSquare Digital website

Static site for **https://www.truesquaredigital.com** (GitHub Pages).

## Includes
- Home + Games catalog (Sit Tight live; coming-soon cards)
- Privacy Policy + Terms of Use (ported from Google Sites)
- Support page
- Root `app-ads.txt` for AdMob (`pub-5155911610089674`)
- `robots.txt` that **allows** crawling (fixes AdMob robots block)
- YouTube: https://www.youtube.com/@TrueSquareDigital

## Publish (GitHub Pages)
1. Create a public GitHub repo (e.g. `TSQMain/truesquaredigital-site` or `truesquaredigital.github.io`).
2. Push this folder to `main`.
3. Settings → Pages → Deploy from branch `main` / `/ (root)`.
4. Custom domain: `www.truesquaredigital.com` (CNAME file already present).
5. At Namecheap (or your registrar), replace Google Sites DNS with GitHub Pages records:
   - **www** CNAME → `YOURUSER.github.io` (or org pages host GitHub shows)
   - Apex `truesquaredigital.com`: GitHub A records (or ALIAS/ANAME if supported), and optionally redirect apex → www
6. Remove old Google Sites / URL redirects that rewrite `/app-ads.txt`.
7. In Play Console, developer website must match the domain AdMob crawls (prefer `https://www.truesquaredigital.com` or apex — keep consistent with where `app-ads.txt` lives).
8. AdMob → App-ads.txt → request crawl of `https://www.truesquaredigital.com/app-ads.txt`.

## Local preview
Open `index.html` via any static server from this folder, e.g. `python3 -m http.server 8080`.
