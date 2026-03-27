# Public Test Blueprint Catalog

This directory is a minimal Git repository scaffold for testing `BlueprintCatalog`
inspect and sync from a public Git source.

Copy the contents of this directory into a new public GitHub repository and push
it to `main`. The current prototype reads repo metadata and blueprint entries
from `catalog/index.yaml`, then resolves each entry's source location before
materializing `Blueprint` resources.

## Layout

- `catalog/blueprints/*/blueprint.yaml`
  Example blueprint manifests referenced by `catalog/index.yaml`.
- `catalog/index.yaml`
  Catalog descriptor used for preview metadata and entry resolution.
- `catalog/bundles/`
  Placeholder for future published bundle manifests.
- `cluster/blueprintcatalog.example.yaml`
  Example cluster-side `BlueprintCatalog` manifest. Update the repo URL before
  applying it.

## Suggested Publish Flow

1. Create a new public GitHub repository.
2. Copy this directory's contents to the new repository root.
3. Update `cluster/blueprintcatalog.example.yaml` with the new GitHub URL.
4. Commit and push to `main`.
5. Apply the example `BlueprintCatalog` manifest to your test cluster.
6. Inspect the repository from the UI.
7. Review the preview metadata and discovered blueprints.
8. Save the repository and request a sync from the UI or with:

```bash
kubectl annotate blueprintcatalog public-test \
  catalog.suse.ai/reconcile-requested-at="$(date -u +%FT%TZ)" --overwrite
```

## Expected Sync Result

This scaffold includes three indexed blueprints:

- `assistant-starter`
- `rag-workbench`
- `inference-lab`

After sync completes, the catalog should report `blueprintCount: 3` and those
three `Blueprint` resources should exist in the cluster with catalog ownership
labels added by the controller.
