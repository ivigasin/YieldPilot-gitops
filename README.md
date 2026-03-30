# FlowFi GitOps Repository Template

This template models the separate GitOps repository consumed by Argo CD.

- `base/` mirrors `infra/k8s/base` (Deployments, Services, ConfigMap).
- `overlays/dev` and `overlays/staging` set namespace + **DigitalOcean Container Registry** image names (`registry.digitalocean.com/vigasin-flowfi/flowfi/*`). Change `vigasin-flowfi` if your registry name differs.
- CI in the app repository updates overlay image tags; Argo CD reconciles.

## Promotion model

1. Build and push images in app repo CI.
2. Update image tags in `overlays/<env>/kustomization.yaml`.
3. Commit and push to GitOps repository.
4. Argo CD ApplicationSet auto-sync applies the change.
