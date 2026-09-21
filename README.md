# Neoleaf app associations

Public association files for `https://auth.neoleaf.studio`.

## Endpoint

`https://auth.neoleaf.studio/.well-known/apple-app-site-association`

The `webcredentials.apps` list contains True Golf: `WDF3M2WTXZ.dev.neoleaf.truegolf`, from its Xcode signing configuration. Confirm the signed application identifier if its App ID prefix differs from its team ID.

## Cloudflare Pages deployment

Upload `.well-known/apple-app-site-association`, `_headers`, and `index.html` together, retaining their paths. `_headers` sets the association endpoint's Content-Type to `application/json` and a five-minute cache lifetime. Register `auth.neoleaf.studio` as a custom domain in Pages, then replace the GoDaddy `auth` CNAME with the exact Pages hostname assigned to this project.

The endpoint must return HTTP 200 directly over valid HTTPS with the expected JSON and no redirect. Verify the public endpoint and Apple's association lookup before relying on it in an app.

This is a direct-upload setup: commits to this repository do not automatically deploy to Cloudflare. Upload a fresh bundle when changing app identifiers.

## Migration status

Cloudflare Pages project `neoleaf-auth` is deployed at `https://neoleaf-auth.pages.dev`. Its association endpoint was verified to return HTTP 200 over HTTPS, Content-Type `application/json`, and the expected True Golf app identifier.

GoDaddy DNS now points `auth.neoleaf.studio` to `neoleaf-auth.pages.dev`. The authoritative nameserver and public resolvers 1.1.1.1 and 8.8.8.8 confirmed the new CNAME. Cloudflare custom-domain verification has been initiated; custom-domain HTTPS and Apple association lookup remain pending.

The former GitHub Pages deployment is temporarily retained for cached DNS during the transition. `CNAME` and `.nojekyll` support that fallback. GitHub Pages serves the extensionless file as `application/octet-stream` and does not support a per-file override.

## Adding apps

Add each approved app's exact application identifier to `webcredentials.apps`. Configure the associated-domain entitlement and passkey relying-party ID consistently with its authentication backend. Publishing this file does not enable passkeys or merge accounts across Supabase projects. A shared relying-party ID defines a shared credential scope; use per-app relying-party subdomains if credential isolation is required.

The host can change without changing the domain or path. Prepare HTTPS on the replacement host before switching DNS, and retain the old host during DNS propagation.

Never commit credentials, signing keys, Supabase secrets, or user data here.
