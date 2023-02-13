
-----
```
cat <<EOF | kubectl apply -f -
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: vclusters
  namespace: argocd
  finalizers:
  - resources-finalizer.argocd.argoproj.io
spec:
  project: default
  sources:
  - repoURL: https://github.com/luvres/platform/vcluster.git
    path: exacta
    targetRevision: HEAD
  destination:
    namespace: vclusters
    name: in-cluster
  syncPolicy:
    automated:
      selfHeal: true
      prune: true
EOF
```
