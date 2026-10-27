# AGENTS.md

Canonical instructions for every agent (Codex and Claude) in this repo.
`CLAUDE.md` imports this file; edit it here. Open work is GitHub issues.

## Project

VibeTrunk is a hub for small, independent tools and games. This repo is its
landing page at the root domain `vibetrunk.com`: one static page that lists
and links every tool. `README.md` has the current state and how to add a tool.

- Stack: Astro, static output, no client-side JavaScript, no backend.
- Hosting: Vercel project `home`, on the apex `vibetrunk.com` (`www`
  redirects). DNS is at Porkbun.
- Ecosystem, for context only: every tool has its own repo in the
  `VBTRNK` org, its own Vercel project and a subdomain. Tools that need a
  backend share one Supabase project, one Postgres schema per tool. This repo
  knows a tool only by its name, blurb and URL in `src/data/tools.ts`.
- New tools start from the `vibetrunk-new-tool` skill, not by copying this
  repo.
- A hobby project and a deliberate learning project in production-grade
  practice: clear structure, decisions recorded in `docs/decisions.md`.

## Invariants

- No secret in a tracked file, a log or the built output.
- The Content-Security-Policy in `vercel.json` stays strict (`script-src
  'none'`, no `unsafe-inline`); loosen it per origin, never with a wildcard.

Changing a rule, invariant or public contract means recording it in
`docs/decisions.md`.

## Commands

- `npm install`, `npm run dev`, `npm run build`, `npm run preview`,
  `npm run check` (type-check). Node >= 22.12.

## Workspace and branches

- `main` is protected: squash merges only, `scan` (gitleaks) must pass.
  Branch (`feat/`, `fix/`, `docs/`, ...) and open a PR; the owner reviews and
  merges. Branches auto-delete on merge. Use conventional commit prefixes.
- Never commit, push, deploy or change hosted state without the owner's
  authorization for that change.

## Release

A merge to `main` deploys to production through Vercel's Git integration. The
merge authorizes that deploy only; other hosted changes need their own yes.
Never run `vercel deploy` or `vercel --prod` by hand unless asked.

## Agent safety

- Hooks in `.claude/hooks/` and `.codex/hooks/` block destructive commands
  (forced deletes, force push, remote branch deletion, hard reset, forced
  clean, broad checkout discards, forced branch deletion, downloads piped into
  an interpreter). What they enforce is non-negotiable; changing a guard needs
  a PR the owner asked for. Codex hooks and rules need the repo to be trusted.
- Never auto-allowed: `git commit`, `git push`, state-changing `gh` commands
  (merge, close, comment, rerun, cancel, delete).
- Dependabot waits 5 days after a release; review any manual install in its
  PR diff.

## Documentation map

`README.md` is the current state, `docs/decisions.md` the rules and their
reasons, GitHub issues the open work, and the PR description the narrative.
