# Neoleaf app associations

Public static files for `https://auth.neoleaf.studio`, hosted with GitHub Pages.

## Published endpoint

`https://auth.neoleaf.studio/.well-known/apple-app-site-association`

The `webcredentials.apps` list currently contains True Golf: `WDF3M2WTXZ.dev.neoleaf.truegolf`, from its Xcode signing configuration. Confirm the signed application identifier if its App ID prefix differs from its team ID.

## Hosting

Publish the `main` branch root through GitHub Pages. `.nojekyll` preserves the `.well-known` directory. `CNAME` configures `auth.neoleaf.studio`; its DNS CNAME must point to `cmlunn.github.io`. Enable Enforce HTTPS after GitHub provisions the certificate.

The association endpoint must return HTTP 200 directly over HTTPS, without redirects. Do not add a `.json` extension to the filename.

## Adding apps

Add each approved app's exact application identifier to `webcredentials.apps`. Each app must configure its associated-domain entitlement and passkey relying-party ID consistently with its authentication backend. Publishing this file alone does not enable passkeys or merge accounts across separate Supabase projects. A shared relying-party ID defines a shared credential scope; choose per-app relying-party subdomains if credential isolation is required.

Never commit credentials, signing keys, Supabase secrets, or user data here.
