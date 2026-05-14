# sbrs-docsite

Documentation website for **[Spring Batch RS](https://crates.io/crates/spring-batch-rs)** — a Rust toolkit for building enterprise-grade batch applications.

Live at: **https://spring-batch-rs.boussekeyt.dev/**

Built with [Astro](https://astro.build/) + [Starlight](https://starlight.astro.build/).

## Commands

```bash
# Install dependencies
yarn install

# Start dev server at http://localhost:4321
yarn dev

# Production build
yarn build

# Preview production build locally
yarn preview
```

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

## Content Rules

**All pages must be `.mdx` files** — never `.md`. A `.md` file silently shadows an `.mdx` file with the same name, breaking the page.

Every page requires this frontmatter:

```mdx
---
title: Clear, Short Title
description: One sentence for SEO and nav previews.
sidebar:
  order: <number>
---
```

Code blocks must specify a language and include the matching `cargo run` command:

````mdx
```rust title="examples/csv_processing.rs"
// code here
```

```bash
cargo run --example csv_processing --features csv
```
````

## Deployment

Deployed to **Firebase Hosting** via GitHub Actions:

- Push to `main` → deploys to production
- Pull request → deploys a preview channel

The Firebase project ID is `spring-batch-rs`. The secret `FIREBASE_SERVICE_ACCOUNT_SPRING_BATCH_RS` must be set in the repository's GitHub Actions secrets.

## Sync with sbrs-lib

When the Rust library changes, update the corresponding pages here:

| sbrs-lib change | Pages to update |
|---|---|
| New reader / writer | `item-readers-writers/overview.mdx` + `reference/features.mdx` |
| New tasklet | `tasklets/` + `reference/features.mdx` |
| New example | `examples/<category>.mdx` |
| New feature flag | `reference/features.mdx` |
| Version bump | Version badge in `index.mdx` |
