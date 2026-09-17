# oscd-plugins-registry

A static registry of OpenSCD plugin providers, published as a `providers.json`
file over GitHub Pages.

## What is this?

[`compas-bearingpoint-plugins`](https://github.com/stee-re/compas-bearingpoint-plugins)'
`Plugin-Hub`, and other OpenSCD hosts, discover plugins from third-party
**providers**. Each provider is a small JSON object describing where to find
that provider's `plugins.json` manifest:

```json
{
  "prefix": "OE",
  "name": "OmicronEnergy Plugins",
  "icon": "https://omicronenergyoss.github.io/oscd-explorer/omicronenergy.png",
  "description": "Official OmicronEnergy plugin provider for OpenSCD.",
  "pluginsUrl": "https://omicronenergyoss.github.io/oscd-explorer/omicronenergy.plugins.json"
}
```

This repo contains no application code — only [`providers.json`](providers.json),
an array of such provider entries. `npm run build` copies it, as-is, into `dist/`;
`npm run deploy` (via `oscd-tooling`'s `oscd deploy`, which wraps
[`gh-pages`](https://www.npmjs.com/package/gh-pages)) publishes `dist/` to the
`deploy` branch — the same branch convention used by this org's other repos
(see [`oscd-gh-workflows`](https://github.com/OMICRONEnergyOSS/oscd-gh-workflows)).

[`.github/workflows/pages.yml`](.github/workflows/pages.yml) runs that exact same
`npm run build && npm run deploy` on every push to `main`, so pushing to `main`
republishes automatically. Anyone with push access can also run `npm run build`
then `npm run deploy` locally to publish out-of-band, or trigger the workflow
manually (`workflow_dispatch`).

One-time setup: Settings → Pages → Source: **Deploy from a branch**, branch
`deploy` / `(root)` (created on first deploy).

Once enabled, the file is served at:

```
https://omicronenergyoss.github.io/oscd-plugins-registry/providers.json
```

Consumers fetch that URL directly and load each entry's `pluginsUrl` in turn.

## Adding / updating a provider

1. Edit `providers.json` and add/update an entry.
2. Open a PR; once merged to `main`, the Pages deploy workflow republishes it automatically.
   Alternatively, run `npm run build && npm run deploy` locally.

## License

[Apache-2.0](LICENSE)
