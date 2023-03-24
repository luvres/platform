# GitOps

### Create namespace
```
kubectl create namespace visstorymaker
```
# Create Project
```
cat <<EOF | kubectl apply -f -
apiVersion: argoproj.io/v1alpha1
kind: AppProject
metadata:
  name: visstorymaker
  namespace: argocd
spec:
  clusterResourceWhitelist:
  - group: '*'
    kind: '*'
  destinations:
  - namespace: '*'
    server: '*'
  sourceRepos:
  - '*'
EOF
```
### Git access
```
cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Secret
metadata:
  name: repo-azure
  namespace: argocd
  labels:
    argocd.argoproj.io/secret-type: repository
stringData:
  type: git
  url: https://exactapucrio@dev.azure.com/exactapucrio/Petrobras%20-%20Smart%20Frete/_git/gitops
data:
  username: bGVvbmFyZG8=
  password: NG5mczNxd3libWhqNjJveDRhM3V4czM3Z2dzNHlucXd2YW1sNmNqZ2VodnF3b2h6emY0cQ==
type: Opaque
#echo -n "leonardo" | base64
#echo -n "iniu6vxiqeklior3sn36p7x4gujqlhp64bakfgkdk2gsgihy2n3q" | base64
EOF
```
### Create namespace
```
kubectl create namespace smartfreight
```
### Create application argocd

```
cat <<EOF | kubectl apply -f -
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: smartfreight
  namespace: argocd
  finalizers:
  - resources-finalizer.argocd.argoproj.io
spec:
  project: smartfreight
  sources:
  # Authserver
  - repoURL: https://exactapucrio@dev.azure.com/exactapucrio/Petrobras%20-%20Smart%20Frete/_git/gitops
    path: AuthServer
    targetRevision: HEAD
  # Historic
  - repoURL: https://exactapucrio@dev.azure.com/exactapucrio/Petrobras%20-%20Smart%20Frete/_git/gitops
    path: Historic
    targetRevision: HEAD
  # Calculator
  - repoURL: https://exactapucrio@dev.azure.com/exactapucrio/Petrobras%20-%20Smart%20Frete/_git/gitops
    path: Calculator
    targetRevision: HEAD
  # Railway
  - repoURL: https://exactapucrio@dev.azure.com/exactapucrio/Petrobras%20-%20Smart%20Frete/_git/gitops
    path: Railway
    targetRevision: HEAD
  # Duct
  - repoURL: https://exactapucrio@dev.azure.com/exactapucrio/Petrobras%20-%20Smart%20Frete/_git/gitops
    path: Duct
    targetRevision: HEAD
  # React
  - repoURL: https://exactapucrio@dev.azure.com/exactapucrio/Petrobras%20-%20Smart%20Frete/_git/gitops
    path: React
    targetRevision: HEAD
  destination:
    namespace: smartfreight
    name: vcluster-smartfreight
  syncPolicy:
    syncOptions:
    - CreateNamespace=true
    automated:
      selfHeal: true
      prune: true
EOF
```
# Delete
```
kubectl --namespace argocd delete applications visstorymaker
```





