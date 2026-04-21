# forgeassembler-web

Static landing site for ForgeAssembler. Deployed to **forgeassembler.app** via
Cloudflare (Workers Assets). The older **forgeassembly.com** domain stays
attached as a secondary alias until it expires.

## Structure

- `index.html` — single-page site: hero, features, how-it-works, requirements,
  cross-links to the rest of the Liquid Releasing family, download CTA.
- `latest-version.json` — version-badge data. Updated automatically by the
  `.github/workflows/sync-version.yml` workflow when a new release lands on
  `liquid-releasing/forgeassembler-releases`.
- Image assets — product branding (`forgeassembler_*`), forge-metaphor icons
  shared with the FunscriptForge site (`anvil.png`, `worktable.png`, etc.),
  Liquid Releasing badge (`Icon-Only-White.svg`).

## Local preview

```bash
# any static server works — python stdlib is fine:
python -m http.server 8080
# open http://localhost:8080
```

## Deployment

Cloudflare Workers Assets watches the `main` branch of this repo. Every push
auto-builds and deploys to `forgeassembler.app` (and the legacy
`forgeassembly.com`). No build step — the site is static HTML + assets.

## Release version badge

The hero's "version" line reads from `latest-version.json` via a small inline
fetch. When the `forgeassembler` release workflow publishes a new tag, it fires
a `repository_dispatch` event against this repo; `sync-version.yml` catches it,
writes the new tag into `latest-version.json`, and commits to `main`. Cloudflare
picks up the new commit and the badge updates within a minute.

## Cross-links

This site cross-links to:

- [funscriptforge.com](https://funscriptforge.com) — FunscriptForge (upstream
  tool for building the clip funscripts ForgeAssembler concatenates)
- ForgeYT release artifacts on GitHub (no separate site yet)

Conversely, `funscriptforge.com` has a ForgeAssembler panel that links back here.

## License

Site content © 2026 Liquid Releasing. ForgeAssembler itself is MIT-licensed —
see the [main repo](https://github.com/liquid-releasing/forgeassembler).
