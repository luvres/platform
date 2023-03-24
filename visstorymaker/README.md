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

# List AppProject
```
argocd proj list
```

# Delete
```
kubectl --namespace argocd delete applications visstorymaker
```





