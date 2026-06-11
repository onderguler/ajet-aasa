# AJet AASA

This repository versions and deploys the Apple App Site Association file used
by `ajet.com` and `www.ajet.com`.

## Published file

Vercel source endpoint:

```text
https://ajet-aasa.vercel.app/.well-known/apple-app-site-association
```

The endpoint is deployed automatically from `main` and returns:

```text
HTTP 200
Content-Type: application/json; charset=utf-8
```

Public application endpoints:

```text
https://ajet.com/.well-known/apple-app-site-association
https://www.ajet.com/.well-known/apple-app-site-association
```

The AJet web/CDN layer must reverse-proxy the public application endpoints to
the Vercel endpoint without returning a redirect.

## Route ownership

| Application | Routes |
| --- | --- |
| Production | Existing production routes such as `/checkin` |
| Development | `/mobile-dev/*` |
| Test | `/mobile-test/*` |
| Pre-production | `/mobile-preprod/*` |
| Pilot | `/mobile-pilot/*` |

Example test link:

```text
https://ajet.com/mobile-test/checkin
```

The CMS `DEEPLINKMANAGEMENT` configuration must map
`/mobile-test/checkin` to the existing `checkin` deep-link ID.

## Validation

```bash
jq empty .well-known/apple-app-site-association
curl -i https://ajet-aasa.vercel.app/.well-known/apple-app-site-association
curl -i https://ajet.com/.well-known/apple-app-site-association
curl -i https://www.ajet.com/.well-known/apple-app-site-association
```

Confirm that each public application endpoint is `200`, has
`Content-Type: application/json`, has no redirect, and contains the current
GitHub version.

Apple and CDN caches can delay AASA changes. Validate on a device after
reinstalling the relevant application.
