# Example Assets

Repo for keeping example assets for blog, etc.

Configuring our main application

Now you need some way to tell Argo CD how to find your three Nginx applications. Do this by creating yet another Application. This pattern is called the App of Apps pattern, where one Application contains the instructions to deploy multiple child Applications.

Create a new Application from the GUI called my-apps with the following configuration:

apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: my-apps
spec:
  destination:
    namespace: default
    server: 'https://kubernetes.default.svc'
  source:
    path: argocd/argocd-apps
    repoURL: 'https://github.com/ubijsk/argocd-example-asset.git'
    targetRevision: HEAD
  project: default
  syncPolicy:
    automated:
      prune: true
      selfHeal: true