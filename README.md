# eshan.in

Static site served by GitHub Pages at <https://eshan.in>. Plain HTML, no build
step — edit a file, push to `main`, and Pages redeploys.

## Layout

```
index.html                          Landing page
calorietracker/privacy/index.html   Privacy policy for the CalorieTracker iOS app
CNAME                               Custom domain (eshan.in) — do not delete
```

The `CNAME` file is what tells GitHub Pages to answer for `eshan.in`. Removing
it silently reverts the site to `spicyavocado.github.io/eshan.in`, which would
break the privacy policy URL registered in App Store Connect.

## DNS

The domain is registered at GoDaddy but its nameservers point at **Cloudflare**,
so records are edited in the Cloudflare dashboard, not GoDaddy.

| Type  | Name    | Value                    | Proxy      |
| ----- | ------- | ------------------------ | ---------- |
| CNAME | `@`     | `spicyavocado.github.io` | DNS only   |
| CNAME | `www`   | `spicyavocado.github.io` | DNS only   |

Cloudflare flattens the apex `CNAME` automatically. The record must stay
**DNS only** (grey cloud) — proxying it prevents GitHub from issuing and
renewing the Let's Encrypt certificate for the custom domain.

## Adding another app's policy

Copy `calorietracker/privacy/index.html` to `<appname>/privacy/index.html`,
rewrite the content for that app, and add a card to `index.html`. The URL
becomes `https://eshan.in/<appname>/privacy/`.
