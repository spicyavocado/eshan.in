# eshan.in

Static site served by GitHub Pages at <https://eshan.in>. Plain HTML, no build
step — edit a file, push to `main`, and Pages redeploys.

## Layout

```
index.html                          Landing page
linkedin/index.html                 Forwards to linkedin.com/in/eshanzain
personal-projects/index.html        Lists the apps (links into /calorietracker/)
calorietracker/privacy/index.html   Privacy policy for the CalorieTracker iOS app
calorietracker/support/index.html   Support page and FAQ
CNAME                               Custom domain (eshan.in) — do not delete
```

Both pages are URLs App Store Connect holds on file — the privacy policy and
the support URL — so they have to keep resolving after release, not just up to
review.

The `CNAME` file is what tells GitHub Pages to answer for `eshan.in`. Removing
it silently reverts the site to `spicyavocado.github.io/eshan.in`, which would
break both of them.

## DNS

The domain is registered at GoDaddy but its nameservers point at **Cloudflare**,
so records are edited in the Cloudflare dashboard, not GoDaddy.

| Type  | Name    | Value                    | Proxy      |
| ----- | ------- | ------------------------ | ---------- |
| CNAME | `@`     | `spicyavocado.github.io` | DNS only   |
| CNAME | `www`   | `spicyavocado.github.io` | DNS only   |
| MX    | `@`     | `mx01.mail.icloud.com` (priority 10) | — |
| MX    | `@`     | `mx02.mail.icloud.com` (priority 10) | — |
| TXT   | `@`     | `v=spf1 include:icloud.com ~all` | — |
| CNAME | `sig1._domainkey` | `sig1.dkim.eshan.in.at.icloudmailadmin.com` | DNS only |

The MX, TXT and DKIM records are for iCloud Mail (hi@eshan.in).

Cloudflare flattens the apex `CNAME` automatically. The record must stay
**DNS only** (grey cloud) — proxying it prevents GitHub from issuing and
renewing the Let's Encrypt certificate for the custom domain.

## Adding another app's policy

Copy `calorietracker/privacy/index.html` to `<appname>/privacy/index.html`,
rewrite the content for that app, and add a card to
`personal-projects/index.html`. The URL
becomes `https://eshan.in/<appname>/privacy/`.
