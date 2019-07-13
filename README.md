# Kustomize Test Case

## What?

- Test case for something not working like expected with `kustomize`

## Structure

- `base` declares a `ServiceAccount`, no namespace is specified
- `overlays/integration` declares a `ClusterRoleBinding` refering the `ServiceAccount` in the `apps-integration` namespace
- `overlays/demo` declares a `ClusterRoleBinding` refering the `ServiceAccount` in the `apps-demo` namespace
- `overlays/both` is a composition of the two previous overlays

## What works

- `kustomize build overlays/integration`
- `kustomize build overlays/demo`

## What fails but is expected to work

- `kustomize build overlays/both`

Error message :

```bash
╰─» asdf global kustomize v2.0.3
╰─» kustomize build overlays/both/
Error: Multiple matches for name ~G_v1_ServiceAccount|apps-integration|~P|faros|~S:
  [~G_v1_ServiceAccount|apps-integration|~P|faros|~S ~G_v1_ServiceAccount|apps-demo|~P|faros|~S]

╰─» asdf global kustomize v2.1.0
╰─» kustomize build overlays/both/
Error: string case - multiple matches for ~G_v1_ServiceAccount|~X|faros:
  [~G_v1_ServiceAccount|apps-demo|faros
 ~G_v1_ServiceAccount|apps-integration|faros
]

╰─» asdf global kustomize v3.0.2
╰─» kustomize build overlays/both/
Error: string case - multiple matches for ~G_v1_ServiceAccount|~X|faros:
  [~G_v1_ServiceAccount|apps-demo|faros
 ~G_v1_ServiceAccount|apps-integration|faros
]

```
