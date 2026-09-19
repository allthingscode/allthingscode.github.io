# allthingscode Workspace CLI OAuth Site

This repository publishes the public homepage and privacy policy required by Google for the personal `allthingscode Workspace CLI` OAuth client.

- Homepage: <https://allthingscode.github.io/>
- Privacy policy: <https://allthingscode.github.io/privacy/>

The site is intentionally static and contains no analytics, cookies, forms, or JavaScript.

## Google OAuth configuration

- Google Cloud project: `allthingscode-workspace`
- OAuth app name: `allthingscode Workspace CLI`
- User type: External
- Publishing status: In production
- Authorized domain: `allthingscode.github.io`

The app was moved from Testing to In production on 2026-09-19 so that its non-basic OAuth refresh token is not subject to the seven-day Testing-mode expiration. This is a personal-use app; do not move it back to Testing during routine maintenance.

## Shared `gws` credential

The encrypted user credential under `C:\Users\HayesChiefOfStaff\.config\gws` is shared by current and future agent sessions. Its required capability baseline is:

- Full Google Tasks, Calendar, Drive, Docs, Sheets, and Slides access.
- Gmail read/modify, compose/send/insert, labels, basic settings, sharing settings, and current-message/current-compose add-on access.
- Cloud Platform access and OpenID email/profile identity.

Do not reauthorize for only one service. If the current credential is still readable, preserve its exact scopes in PowerShell:

```powershell
$scopes = (gws auth status | ConvertFrom-Json).scopes -join ','; gws auth login --scopes $scopes
```

The `gws auth login --services ...` command can present an interactive picker with narrower defaults, so it is only a recovery baseline when the existing scope list is unavailable. After any renewal, require `token_valid: true`, `has_refresh_token: true`, the intended scope set, and a bounded live read from each of Tasks, Calendar, Drive, Gmail, Docs, Sheets, and Slides.

On 2026-09-19, authorization was renewed with all 24 existing scopes preserved and all seven service reads passed.
