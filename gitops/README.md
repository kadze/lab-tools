# gitops

Cluster add-ons this lab needs, one directory per component. No
`kustomization.yaml` here - Flux auto-generates one by scanning
subdirectories recursively, so a new component is picked up without editing
an index file.

Empty for now. Phase 1 adds `gateway-api/`, `cert-manager/` and
`observability/`.
