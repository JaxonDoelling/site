# Personal Site — Design Spec

Date: 2026-07-25

## Purpose

A portfolio-first, blog-secondary personal site for Jaxon Doelling. Showcases
software/dev projects and writing/research, with a resume/about section.
Blog and project content is written in Obsidian and published by pushing to
git — no manual export step.

## Stack

- **Astro** (static site generator) with content collections for
  markdown-based content.
- **Vercel** for hosting, connected to a GitHub repo, auto-deploy on push to
  `main`.
- **Plain CSS** with a small set of design tokens (CSS custom properties) —
  no utility framework. The visual system is bespoke (see below), so
  hand-written tokens give more direct control than a framework's defaults.
- **Fonts**: Geist (sans) for headings/UI/body, Geist Mono for
  labels/dates/tags/code snippets. Both are open-source (SIL license), no
  licensing cost.

## Content model

Two Astro content collections, defined with zod schemas in
`src/content/config.ts`:

- `content/projects/*.md` — frontmatter: `title`, `summary`, `date`, `tags`,
  `repoUrl`, `demoUrl`, `draft`
- `content/posts/*.md` — frontmatter: `title`, `date`, `tags`, `summary`,
  `draft`

Entries with `draft: true` are filtered out of all page queries, so they
never appear in the built site regardless of where they live in the repo.

## Obsidian workflow

- The `content/` folder inside this repo is meant to be (or be symlinked
  from) a folder within an Obsidian vault. Jaxon writes and edits notes
  directly there.
- Recommended: the **Obsidian Git** community plugin for one-click
  commit+push from inside Obsidian. Plain `git` CLI works identically if
  preferred.
- Publish flow: write → commit → push to `main` → Vercel builds and deploys
  automatically. There is no separate export/copy/build step for the user to
  run manually.

## Site structure (information architecture)

- `/` — Home: short intro, name with subtle octopus mark, links to
  Projects/Writing/About
- `/projects` — grid of project cards (bento-style, hairline borders)
- `/projects/[slug]` — individual project case-study page
- `/writing` — blog list: title, date, tags, excerpt
- `/writing/[slug]` — individual post page
- `/writing/rss.xml` — RSS feed
- `/about` — bio, work history, skills, contact links

## Visual design system

Inspired by vercel.com's contrast and layout:

- **Base palette**: near-black background, near-white text, a grayscale
  scale for borders/dividers/secondary text.
- **Layout**: bento-grid sections divided by 1px hairline borders, generous
  padding, a strong alignment grid — not soft cards with shadows.
- **Typography**: Geist for headings/nav/body copy; Geist Mono for
  metadata (dates, tags) and code.
- **Accent**: a single vivid blue used sparingly — links, hover states,
  highlighted tags — doubling as a nod to the blue-ringed octopus branding
  without being literal about it.
- **Components**: pill/bordered buttons with crisp high-contrast states (no
  gradients or drop shadows); cards use hairline borders, not shadows.
- **Logo**: an inline SVG, line-art blue-ringed octopus mark. Used as the
  favicon and as a small mark next to the name in the header — subtle, not a
  large illustration.

## Deployment

- New GitHub repo, pushed to from this project.
- Vercel project connected to that repo; auto-deploy on push to `main`.
- No custom domain yet — use the Vercel-provided subdomain. Custom domain
  can be added later without any code changes.

## Explicitly out of scope for v1

No comments system, no search, no newsletter/email capture. These are easy
to add later if actually wanted; building them now would be speculative.

## Assumptions to confirm

- Display name is "Jaxon Doelling" (inferred from account email) — correct
  if wrong.
