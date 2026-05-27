# sl8-templates

Public registry of the `sl8-*` E2B sandbox templates used by [StartHalo](https://github.com/StartHalo).

> **This repo is a mirror.** The source of truth lives in [`StartHalo/sl8-tools`](https://github.com/StartHalo/sl8-tools) (private). A GitHub Action mirrors `templates.json` (and `templates.schema.json`) here on every template release. Do not edit files in this repo directly — they'll be overwritten on the next sync.

## Endpoints

| URL | Purpose | Cache TTL |
|---|---|---|
| [`templates.json`](https://cdn.jsdelivr.net/gh/StartHalo/sl8-templates@main/templates.json) | The registry — what's available, with versions and tool packs | ~10 min |
| [`templates.schema.json`](https://cdn.jsdelivr.net/gh/StartHalo/sl8-templates@main/templates.schema.json) | JSON Schema (Draft 2020-12) for the registry shape | ~10 min |

All endpoints are served via [jsDelivr](https://www.jsdelivr.com/)'s global CDN. No auth required.

## Quick usage

```ts
const registry = await fetch(
  'https://cdn.jsdelivr.net/gh/StartHalo/sl8-templates@main/templates.json',
).then((r) => r.json())

const anim = registry.templates.find((t) => t.name === 'sl8-animation')
const sandbox = await Sandbox.create(anim.aliases.generic)
```

Full guide (TypeScript, Python, Bash, Go, schema validation, FAQ):
[`docs/guides/e2b-templates-registry/`](https://github.com/StartHalo/sl8-tools/tree/main/docs/guides/e2b-templates-registry) in `sl8-tools`.

## What's in `templates.json`

| Field | Description |
|---|---|
| `schemaVersion` | Currently `1`. Bumps on incompatible shape changes. |
| `generatedAt` | ISO timestamp of the snapshot. |
| `sourceCommit` | The `sl8-tools` commit this snapshot was generated from. |
| `templates[]` | Active `sl8-*` templates — name, aliases, current version, components (for base) or base+packs (for variants). |
| `archivedTemplates[]` | Templates that used to exist, with replacement guidance. |

See [`templates.schema.json`](./templates.schema.json) for the full schema.

## Documentation

- **Consumer guide:** [`docs/guides/e2b-templates-registry/`](https://github.com/StartHalo/sl8-tools/tree/main/docs/guides/e2b-templates-registry) in `sl8-tools`
- **Feature documentation:** [`docs/features/e2b-templates-registry/`](https://github.com/StartHalo/sl8-tools/tree/main/docs/features/e2b-templates-registry) in `sl8-tools`
- **Design history:** [`docs/features/e2b-templates-discovery/`](https://github.com/StartHalo/sl8-tools/tree/main/docs/features/e2b-templates-discovery) in `sl8-tools`

## License

MIT — see [LICENSE](./LICENSE).
