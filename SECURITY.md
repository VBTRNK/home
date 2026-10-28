# Security

This repo is currently a static landing page with no backend, no database,
and no user accounts — there is no user data at risk today.

If you notice something suspicious (a CSP bypass, a vulnerable dependency, a
leaked credential), report it privately through GitHub's
[private vulnerability reporting](https://github.com/VBTRNK/home/security/advisories/new)
rather than opening a public issue.

This policy will be expanded significantly once a VBTRNK-org repo handles
real user data — starting with the Supabase-backed Cogitster
game. See [docs/decisions.md](docs/decisions.md) for the reasoning behind the
current agent-safety and CI scaffolding.
