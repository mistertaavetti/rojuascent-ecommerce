# Rojuascent — Luxury Fashion E-Commerce

> Case study: a luxury fashion e-commerce platform — premium motion design, headless CMS, and payment integration built for a brand where the experience *is* the product.
> **Code is proprietary; this repo documents the build** — architecture, decisions, and outcomes.

---

## Context

| | |
|---|---|
| **Client** | Rojuascent (luxury fashion retail) — via Taavetti Digital |
| **Role** | Full-stack — storefront, CMS, payments, deployment |
| **Timeline** | 2024 — present (deployed to production) |

## Problem

Rojuascent needed to sell fashion online without diluting the brand. Luxury e-commerce lives or dies on feel: scroll-triggered reveals, polished transitions, and high-quality imagery — while the unglamorous fundamentals (catalog, cart, checkout, payments, inventory) have to be absolutely solid underneath.

## Architecture

```
┌─────────────────────────┐        ┌─────────────────────────┐
│  Next.js 15 storefront  │        │  Strapi 4 headless CMS  │
│  React 19, Tailwind 4,  │ ◀────▶ │  Products, media,       │
│  Framer Motion, Redux   │  REST  │  scheduling, sitemap    │
└───────────┬─────────────┘        └─────────────────────────┘
            │ checkout
            ▼
┌─────────────────────────┐
│  Flutterwave payments   │
│  (checkout + webhooks)  │
└─────────────────────────┘
```

### Stack

| Layer | Technology |
|---|---|
| Storefront | Next.js 15.3, React 19, TypeScript 5.8, Tailwind CSS 4 |
| State & forms | Redux Toolkit, React Hook Form |
| Motion | Framer Motion 12 — scroll reveals, viewport-triggered animations, launch countdown |
| CMS | Strapi 4.26 headless (GraphQL, scheduler, sitemap, media plugins) |
| Payments | Flutterwave React V3 — checkout + webhook verification |
| Coming-soon page | React 19 + Vite (pre-launch campaign with countdown + newsletter) |
| Deployment | Docker + Traefik reverse proxy, PM2 process management, production DNS/SSL |

## Key Technical Decisions

| Decision | Rationale | Trade-off |
|---|---|---|
| Next.js over plain React | SEO and shareability matter for product discovery; SSR for catalog pages | Animation work needs care to stay smooth over SSR'd markup |
| Headless CMS (Strapi) | Brand team manages products, images, and content without deploys | Another service to operate; content modeling effort up front |
| Framer Motion for brand motion | Scroll choreography and transitions are the brand experience | Bundle weight and the discipline of respecting reduced-motion preferences |
| Flutterwave for payments | Nigerian market fit for the brand's customer base | International cards/currencies need additional gateway support later |
| Redux Toolkit for cart/catalog state | Predictable state across cart persistence and checkout flows | Boilerplate that lighter state tools wouldn't need at this size |

## Build & Delivery Notes

- Production deployment completed with Docker/Traefik fixes (image URL handling, database credentials via environment, routing labels) — PM2 stable in production since July 2026.
- Launch campaign infrastructure: coming-soon page with countdown timer and newsletter signup.
- Product onboarding (image upload, pricing, categories, variants) is the closing milestone, with a test-coverage track (Jest + Playwright) planned after.

## What I'd Do Differently

- **Image pipeline as a first-class feature.** Product photography is the conversion driver in luxury e-commerce; an automated optimization/CDN pipeline should ship with the catalog, not after it.
- **Test coverage before launch traffic.** Jest + Playwright coverage was planned for after closeout — checkout flows deserve tests from the first sprint.
- **Abandoned-cart recovery in initial scope.** It's the highest-leverage e-commerce automation and wasn't in the first release.

## Evidence

- **Live platform:** available on request.
- **Screenshots:** available on request.

---

*Case study by David Aloba. [code.davidaloba.com](https://code.davidaloba.com) · [LinkedIn](https://linkedin.com/in/mistertaavetti)*
