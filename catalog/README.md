# Catalog

This catalog matches the directory shape expected by the current
`BlueprintCatalog` controller.

## Contents

- `index.yaml`: catalog descriptor used for preview metadata and indexed entries
- `blueprints/`: controller-discovered blueprint manifests
- `bundles/`: optional future bundle manifests

The current prototype uses `index.yaml` for inspect preview and entry resolution.
It currently materializes only `Blueprint` manifests. Bundle materialization is
not part of the current smoke test.
