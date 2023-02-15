
-----
```
cat <<EOF | kubectl apply -f -
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: platform
  namespace: argocd
  finalizers:
  - resources-finalizer.argocd.argoproj.io
spec:
  project: default
  sources:
  - repoURL: https://github.com/luvres/platform.git
    path: .
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

###tree
-----
.
├── ingress
│   └── ingress-exacta.yaml
├── README.md
├── resources.yaml
└── vcluster
    ├── exacta
    │   └── cluster.yaml
    ├── ingress
    │   ├── exacta
    │   │   └── ingress.yaml
    │   └── smartfreight
    │       └── ingress.yaml
    └── smartfreight
        └── cluster.yaml
