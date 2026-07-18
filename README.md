# mindforge-content

Source-of-truth content repo for mindforge's content registry (D52). CI on
`main` builds `registry.json` plus a source tarball per published pack
version and deploys them to GitHub Pages. Portable/cloud installs of
mindforge fetch that ledger to discover and download packs.

## Pack layout

Each top-level directory under `packs/` is one pack, named after its
namespace:

```
packs/<namespace>/
  pack.json          # manifest: namespace, title, description, version,
                      # contractVersion, requires
  concepts/*.md       # concept content, frontmatter + body
  questions/*.yaml    # question banks
  assets/             # optional media referenced by concepts
```

Author packs against the JSON Schemas exported by the app repo:
`app/schemas/pack-manifest.schema.json`, `concept-frontmatter.schema.json`,
`question-file.schema.json` (fetched into this repo's CI checkout at
`app/schemas/`, not vendored here — see the workflow).

## Release flow

1. Bump `version` in the pack's `pack.json` (semver, monotonically
   increasing per namespace).
2. Open a PR with the content change.
3. Merge to `main` — CI (`.github/workflows/publish.yml`) validates every
   pack, packages it into `<namespace>-<version>.tar.gz`, and publishes an
   updated `registry.json` to GitHub Pages.

**Published versions are immutable.** Re-publishing an existing version
with different content is a hard build failure — bump the version instead.
Old tarballs remain available indefinitely; Pages deploys replace the whole
site, so the workflow re-downloads every previously published archive
before rebuilding (see the "Carry forward published archives" step) to
avoid losing history.

## Pinning the app repo

This repo's CI checks out `norwestern/mindforge` at a pinned tag
(`registry-v1`) to get `scripts/build-registry.ts` and the registry
contract/schemas — never `main`, so a breaking change in the app repo can't
silently break this repo's publishes.

To bump the pin after an app-repo contract change:

1. Land and tag the change in `norwestern/mindforge` (new tag, e.g.
   `registry-v2`).
2. Update `ref:` in `.github/workflows/publish.yml` to the new tag.
3. If the change bumps the registry `contractVersion`, bump
   `contractVersion` in this repo's `pack.json` files as required and cut
   new pack versions.

## Until Phase 5

`packs/core` here is a mirror of the app repo's own `packs/core/` — the app
still bundles that pack directly and doesn't yet consume this registry at
runtime. Until Phase 5 (the zero-content flip), any edit to the core pack
lands in the app repo first and gets copied here; don't edit `packs/core`
in this repo directly, it will be overwritten.
