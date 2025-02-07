# argocd-demo

## Umbrella charts

- Current setup gives example of umbrella Helm chart setup but this also works
  with regular Chart as well.

## Upgrading the Chart

1. Pump up `dependencies.verion`
2. run `helm dependency update`
3. commit
4. sync

## Multi-env deployment - Argocd applicationsets

- We can use values-{cluster}.yaml, where cluster can be prod, dev to
  differentiate configuration between environments and in argo applicationsets
  reference values-{cluster}.yaml as deployment target:
  ```yaml
  ...
  spec:
    project: infra
    source:
      repoURL: "https://github.com/CyberCubeAnalyticsInc/sre/tree/dev/kubernetes/eks.git"
      path: prometheus
      targetRevision: "{{targetRevision}}"
      helm:
        valueFiles:
          - values.yaml
          - values-{{cluster}}.yaml
  ```

