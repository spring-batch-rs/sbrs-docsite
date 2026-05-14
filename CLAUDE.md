# CLAUDE.md — sbrs-docsite

Documentation website for **Spring Batch RS**, built with Astro + Starlight.
Live at: https://spring-batch-rs.boussekeyt.dev/

> **Source of content**: The website files originate from `sbrs-lib/website/` and are maintained here as a standalone repo.

## Essential Commands

```bash
# Start dev server (http://localhost:4321)
yarn dev

# Production build
yarn build

# Preview production build locally
yarn preview
```

## Content Rules

### File Format — MDX Only

**All documentation pages MUST be `.mdx` files**, never `.md`.  
A `.md` file in `src/content/docs/` will shadow an existing `.mdx` file with the same stem, breaking the page silently.

### Frontmatter (required on every page)

```mdx
---
title: Clear, Short Title
description: One sentence for SEO and nav previews.
sidebar:
  order: <number>
---
```

### Code blocks

Always specify the language. Add a `title=` attribute when showing a file path:

````mdx
```rust title="examples/csv_processing.rs"
// code here
```
````

Always follow code examples with the matching `cargo run` command:

````mdx
```bash
cargo run --example csv_processing --features csv
```
````

## Content Structure

```
src/content/docs/
├── index.mdx                    # Homepage / splash
├── getting-started.mdx
├── quick-examples.mdx
├── processing-models.mdx
├── architecture.mdx
├── error-handling.mdx
├── item-readers-writers/
│   └── overview.mdx
├── tasklets/
├── examples/
├── tutorials/
├── reference/
│   └── features.mdx
└── api/
```

## Sync with sbrs-lib

This site documents the Rust library in `../sbrs-lib`. When the library changes, update the corresponding pages here:

| sbrs-lib change | Pages to update here |
|---|---|
| New reader / writer | `item-readers-writers/overview.mdx` + `reference/features.mdx` |
| New tasklet | `tasklets/` + `reference/features.mdx` |
| New example | `examples/<category>.mdx` |
| New feature flag | `reference/features.mdx` |
| Version bump | Any version badge or tagline in `index.mdx` |

## Deployment

The site is configured for multiple targets (Firebase, Netlify, nginx). Deployment config files:
- `firebase.json` — Firebase Hosting
- `netlify.toml` — Netlify
- `nginx.conf` + `Dockerfile` — self-hosted container
