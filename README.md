# BlackRoad Interactive — `blackroad-interactive.github.io`

> **Production marketing page** for the BlackRoad Interactive division of BlackRoad OS, Inc.  
> Live at **[blackroad-interactive.github.io](https://blackroad-interactive.github.io)**

[![Deploy: GitHub Pages](https://img.shields.io/badge/deploy-GitHub%20Pages-222?logo=githubpages)](https://blackroad-interactive.github.io)
[![License: Proprietary](https://img.shields.io/badge/license-Proprietary-red)](./LICENSE)
[![Platform: BlackRoad OS](https://img.shields.io/badge/platform-BlackRoad%20OS-673AB7)](https://blackroad.io)

---

## Index

1. [Overview](#1-overview)
2. [Repository Structure](#2-repository-structure)
3. [Deployment](#3-deployment)
4. [npm Packages](#4-npm-packages)
5. [Stripe Integration](#5-stripe-integration)
6. [CI / Continuous Engine](#6-ci--continuous-engine)
7. [End-to-End (E2E) Checklist](#7-end-to-end-e2e-checklist)
8. [Contributing](#8-contributing)
9. [License](#9-license)

---

## 1. Overview

This repository hosts the **official public-facing marketing page** for BlackRoad Interactive — the game-engine and interactive-experience division of [BlackRoad OS, Inc.](https://blackroad.io)

The page is a single, dependency-free static `index.html` served via GitHub Pages. It communicates the division's product focus (game engines, 3D/WebGL, 2D frameworks, and interactive experiences) and links visitors to the broader BlackRoad ecosystem.

**Key facts:**

| Property | Value |
|---|---|
| URL | `https://blackroad-interactive.github.io` |
| Stack | Static HTML · CSS (inline) · Zero JS dependencies |
| Hosting | GitHub Pages (branch: `main`, root `/`) |
| Organization | [BlackRoad-Interactive](https://github.com/BlackRoad-Interactive) |
| Parent company | BlackRoad OS, Inc. |

---

## 2. Repository Structure

```
blackroad-interactive.github.io/
├── index.html          # Production marketing page (single-file, no build step)
├── README.md           # This document
├── LICENSE             # BlackRoad OS, Inc. Proprietary License v2
├── .nojekyll           # Disables Jekyll processing on GitHub Pages
└── .github/
    └── workflows/
        └── continuous-engine.yml   # Perpetual agent heartbeat workflow
```

---

## 3. Deployment

The site is deployed automatically by GitHub Pages on every push to the `main` branch.

**No build step is required.** `index.html` is served directly from the repository root.

### Local preview

```bash
# Any static file server works. Examples:

npx serve .
# or
python3 -m http.server 8080
# then open http://localhost:8080
```

### Production URL

```
https://blackroad-interactive.github.io
```

---

## 4. npm Packages

BlackRoad Interactive publishes and consumes npm packages as part of the broader BlackRoad OS platform. The packages relevant to this page and its ecosystem are listed below.

| Package | Registry | Description |
|---|---|---|
| `@blackroad/engine-core` | [npmjs.com](https://www.npmjs.com/org/blackroad) | Core game-engine runtime |
| `@blackroad/renderer-3d` | [npmjs.com](https://www.npmjs.com/org/blackroad) | WebGL/3D rendering layer |
| `@blackroad/renderer-2d` | [npmjs.com](https://www.npmjs.com/org/blackroad) | Canvas/2D framework |
| `@blackroad/ui` | [npmjs.com](https://www.npmjs.com/org/blackroad) | Shared UI component library |
| `@blackroad/sdk` | [npmjs.com](https://www.npmjs.com/org/blackroad) | Universal developer SDK |

> **Scope:** All BlackRoad npm packages are published under the `@blackroad` organization scope.  
> Install any package with:
> ```bash
> npm install @blackroad/<package-name>
> ```

---

## 5. Stripe Integration

BlackRoad OS, Inc. uses **Stripe** for payment processing across its commercial products and developer subscriptions.

### Integration points

| Surface | Stripe feature |
|---|---|
| Developer subscriptions | Stripe Billing / Subscriptions |
| One-time purchases | Stripe Payment Intents |
| Marketplace payouts | Stripe Connect (Express) |
| Invoicing | Stripe Invoicing API |
| Tax compliance | Stripe Tax |

### Configuration (non-public repos)

Stripe keys are **never** committed to this or any BlackRoad repository. All secrets are managed via:

- **GitHub Actions secrets** for CI/CD pipelines
- **Environment variables** injected at runtime on production servers
- **Stripe Dashboard** for webhook endpoint registration

> ⚠️ If you discover a committed Stripe key, treat it as a security incident and rotate it immediately via the [Stripe Dashboard](https://dashboard.stripe.com/apikeys).

---

## 6. CI / Continuous Engine

The repository includes a self-healing perpetual workflow (`.github/workflows/continuous-engine.yml`) that maintains the BlackRoad agent fleet heartbeat.

| Trigger | Frequency |
|---|---|
| `schedule` (cron) | Every 5 minutes (boot / self-heal) |
| `workflow_dispatch` | Manual, with `chain_count` input |

The workflow runs on `self-hosted` runners tagged `blackroad-fleet` and chains itself on completion to achieve a near-continuous execution loop.

---

## 7. End-to-End (E2E) Checklist

Use this checklist before every production deployment of this page.

- [ ] `index.html` passes [W3C HTML Validator](https://validator.w3.org/)
- [ ] Page loads in <2s on a simulated 3G connection (Chrome DevTools → Network throttling)
- [ ] All external links resolve (GitHub org, `blackroad.io`)
- [ ] Fonts load correctly from Google Fonts CDN
- [ ] Hero animation, grid scroll, and shimmer render on Chrome, Firefox, and Safari
- [ ] `<meta>` Open Graph tags render correctly (test via [opengraph.xyz](https://www.opengraph.xyz/))
- [ ] Mobile layout is correct at 375 px, 414 px, and 768 px viewports
- [ ] No browser console errors (resource load failures, CSP violations, render errors)
- [ ] GitHub Pages deployment is live within 2 minutes of push to `main`
- [ ] Stripe webhook endpoints (in related services) return `200 OK`
- [ ] npm package registry entries are reachable for all `@blackroad` packages

---

## 8. Contributing

This repository is **proprietary**. External contributions are not accepted.

Internal contributors must:

1. Branch from `main` using the naming convention `feature/<description>` or `fix/<description>`.
2. Obtain at least one peer review before merging.
3. Verify the [E2E checklist](#7-end-to-end-e2e-checklist) is fully complete before merging.
4. Never commit secrets, API keys, or credentials.

---

## 9. License

© 2026 BlackRoad OS, Inc. All rights reserved.

This repository is governed by the **BlackRoad OS, Inc. Proprietary License v2**. See [LICENSE](./LICENSE) for the full terms. Unauthorized use, reproduction, or distribution is strictly prohibited.

