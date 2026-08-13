# lab-tools

My personal Istio lab: GitOps config and demo workloads, reconciled by the
`u25c-shared` cluster's existing Flux install (owned by
[`gitops-flux`](https://github.com/Ubuntu-25c-market-prep/gitops-flux)).

This is not a team repo. Istio itself lives in `gitops-flux` under my
`[istio]` epic ([`ops-program#21`](https://github.com/Ubuntu-25c-market-prep/ops-program/issues/21)).
Everything here is the throwaway scaffolding around it - demo apps, load
generation, a lab-scoped observability stack - so it can be created and
destroyed without the team paying for idle resources.

## The switch

```bash
kubectl apply -f bootstrap/    # brings up everything below
kubectl delete -f bootstrap/   # tears it all down (prune: true)
```

`bootstrap/` registers this repo as a `GitRepository` and reconciles
`./gitops` as a `Kustomization`, both named `lab-tools` in `flux-system` so
they sit alongside the team's own Flux objects without colliding.

## Layout

```
bootstrap/     the on/off switch (GitRepository + root Kustomization)
gitops/        cluster add-ons this lab needs, one directory per component
apps/          demo workloads used in the exercises
```

No `kustomization.yaml` at `gitops/` itself - Flux auto-generates one by
scanning subdirectories, same as the team repo.

## Namespace convention

Everything here runs in `lab-*` namespaces (`lab-observability`, `lab-demo`),
never `platform-*`. The `@monitoring` workstream owns `platform-monitoring`
and will land the real kube-prometheus-stack there eventually; keeping mine
in `lab-observability` means the two never collide and mine deletes cleanly
whenever I want.

## Related

- [`kadze/lab-infra`](https://github.com/kadze/lab-infra) - the Terraform
  half: IRSA roles and anything else that isn't a Kubernetes object.
- [`gitops-flux`](https://github.com/Ubuntu-25c-market-prep/gitops-flux) -
  Istio itself, under `infrastructures/*/istio-base`, `istiod`,
  `istio-gateway`.
