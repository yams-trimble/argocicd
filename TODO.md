apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: flask-app
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://github.com/yourusername/argocicd.git  # Replace with your Git repo URL
    targetRevision: main
    path: helm-chart
    helm:
      releaseName: flask-app
      valueFiles:
      - values.yaml
  destination:
    server: https://kubernetes.default.svc  # In-cluster; change for remote
    namespace: flask
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
    syncOptions:
    - CreateNamespace=true
