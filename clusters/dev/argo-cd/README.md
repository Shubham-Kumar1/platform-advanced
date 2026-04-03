# Argo CD Installation (Bootstrap)

Argo CD is installed as a **cluster bootstrap dependency** and is not managed by GitOps.

## Installation Command

Argo CD was installed using the official Helm chart with an explicit version and CRD handling:

```bash
helm install argocd argo/argo-cd \
  --namespace argocd \
  --version 9.4.17 \
  --set crds.install=true \
  --set crds.keep=true \
  --wait
