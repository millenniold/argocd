# ArgoCD

## Introduction

This project is intended to provide a way to play and test basic functionality of ArgoCD.  ArgoCD will be setup in a MiniKube cluster so it can be tested locally.

``` bash
# Start a fresh Kubernetes cluster
minikube start 

# Install ArgoCD on your cluster
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'

# Get the password for accessing ArgoCD UI
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

# Create route to access UI in your browser.  In a separate terminal run the following command and leave it alone
kubectl port-forward svc/argocd-server -n argocd 8080:443

# Open your browser and go to localhost:8080.  Enter 'admin' for the username and the password that was decoded in previous step.
```


