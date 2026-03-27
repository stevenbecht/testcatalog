# Public Test Blueprint Catalog

This directory is a minimal Git repository scaffold for testing `BlueprintCatalog`
sync from a public Git source.

Copy the contents of this directory into a new public GitHub repository and push
it to `main`. No repo-side catalog index is required. The current
`BlueprintCatalog` controller discovers `catalog/blueprints/*/blueprint.yaml`
directly from Git.

## Layout

- `catalog/blueprints/*/blueprint.yaml`
  The controller discovers and materializes these into `Blueprint` resources.
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
6. Request a sync from the UI or with:

```bash
kubectl annotate blueprintcatalog public-test \
  catalog.suse.ai/reconcile-requested-at="$(date -u +%FT%TZ)" --overwrite
```

## Expected Sync Result

This scaffold includes three blueprints:

- `assistant-starter`
- `rag-workbench`
- `inference-lab`

After sync completes, the catalog should report `blueprintCount: 3` and those
three `Blueprint` resources should exist in the cluster with catalog ownership
labels added by the controller.
