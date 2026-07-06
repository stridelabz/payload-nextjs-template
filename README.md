# Payload + Nextjs Template

A Payload CMS + Next.js website based on the official Payload Website Template, adapted for this project with an updated frontend stack and Bun-first workflow.

## Stack

- [Payload CMS 3](https://payloadcms.com/) for the CMS, admin panel, collections, globals, access control, previews, redirects, SEO, search, and scheduled publishing
- [Next.js App Router](https://nextjs.org/) for the frontend and server-rendered routes
- [React 19](https://react.dev/) and [TypeScript](https://www.typescriptlang.org/)
- [Postgres](https://www.postgresql.org/) via `@payloadcms/db-postgres`
- [Tailwind CSS 4](https://tailwindcss.com/)
- [shadcn](https://ui.shadcn.com/) with the `base-nova` style and `lucide` icons
- [Biome](https://biomejs.dev/) for formatting, linting, and import organization
- [Bun](https://bun.sh/) as the primary package manager and script runner

## What changed from the official template

This repo started from Payload's official website template, but the local tooling has been modernized:

- Bun is the main package manager.
- ESLint and Prettier have been replaced by Biome.
- Dependencies have been updated, including Next.js, React, Payload, Tailwind, and shadcn.
- shadcn is configured through `components.json` using the `base-nova` style.

## Quick start

### Prerequisites

- Bun `^1.3.0`
- Node.js `^18.20.2` or `>=20.9.0`
- A Postgres database

### Setup

```bash
bun install
cp .env.example .env
bun dev
```

Open [`http://localhost:3000`](http://localhost:3000) in your browser.

On first run, follow the Payload admin setup flow to create the first admin user.

## Payload features

This project keeps the main features from the Payload website template:

- Auth-enabled users with admin access
- Drafts, versions, draft preview, and live preview
- Layout builder blocks for flexible pages and posts
- Media uploads with image handling
- Categories for content taxonomy
- Header and footer globals
- SEO plugin integration
- Search plugin integration
- Redirects plugin integration
- On-demand revalidation for frontend updates
- Jobs queue and scheduled publishing support

## Content model

### Collections

- `Users` — admin users and authenticated CMS access
- `Pages` — layout-builder pages with drafts and previews
- `Posts` — publishable editorial content
- `Media` — uploads for images, videos, downloads, and other assets
- `Categories` — nested taxonomy for posts
- `Redirects` — managed redirects for changed or migrated URLs
- `Search` — indexed content for frontend search

### Globals

- `Header` — frontend navigation and header data
- `Footer` — footer navigation and site-wide footer data

## Working with Postgres

Payload's Postgres adapter uses a strict schema. During local development, schema push can be convenient, but be careful when pointing at shared or production databases.

For production or shared environments, prefer migrations.

Create a migration locally:

```bash
bun run payload migrate:create
```

Run pending migrations:

```bash
bun run payload migrate
```

## Seeding

You can seed the database from the Payload admin panel using the seed database action.

The seed data may include demo content and a demo author account:

- Email: `demo-author@payloadcms.com`
- Password: `password`

> Seeding is destructive. It can wipe current database content before loading the seed data. Only seed a new database or one you can afford to reset.

## Production

Build and start the app with Bun:

```bash
bun build
bun start
```

Before deploying, make sure environment variables are configured and migrations have been run against the target database.

## Deployment

Deploy this as a standard Next.js + Payload app. Common targets include Vercel, Payload Cloud, a VPS, DigitalOcean Apps, or Coolify.

If deploying to Vercel, you can use Payload's Vercel Postgres and Blob Storage adapters when needed:

```bash
bun add @payloadcms/db-vercel-postgres @payloadcms/storage-vercel-blob
```

See the Payload deployment docs for provider-specific details: <https://payloadcms.com/docs/production/deployment>

## References

- Payload docs: <https://payloadcms.com/docs>
- Next.js docs: <https://nextjs.org/docs>
- Biome docs: <https://biomejs.dev/guides/getting-started/>
- shadcn docs: <https://ui.shadcn.com/docs>
