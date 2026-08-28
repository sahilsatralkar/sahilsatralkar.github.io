# Pending Cloudflare Action

## Cleaning Schedule Legal Pages

**Status:** Pending Cloudflare account configuration. This does not affect the
completed `en-GB` document-language correction.

Disable Cloudflare Web Analytics for `sahilsatralkar.com` requests matching
`/apps/cleaning-schedule/*`. Configure this in Cloudflare Web Analytics or a
Configuration Rule, not in the Jekyll site source.

Before closing this action, verify that each of these pages loads neither
`static.cloudflareinsights.com/beacon.min.js` nor makes a request to
`/cdn-cgi/rum`:

- `/apps/cleaning-schedule/terms`
- `/apps/cleaning-schedule/privacy`
- `/apps/cleaning-schedule/support`
