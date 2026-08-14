# gitops-issuers

Resources that depend on a chart in ../gitops/ actually finishing its Helm
install, not just the HelmRelease object being created - see the ordering
note in bootstrap/kustomization-issuers.yaml.

Empty for now. cert-manager's ClusterIssuer moved to the team's own
cert-manager (gitops-flux#14) once it landed - lab-only TLS should not
depend on a personal, freely-destroyable install.
