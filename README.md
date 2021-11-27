![passing](https://github.com/bradmccoydev/argo-demo/actions/workflows/ci.yml/badge.svg) ![GitHub](https://img.shields.io/github/license/bradmccoydev/argo-demo)
# Argo Demo
This Repo is for a Demo of ArgoCD

# Configuration / Installation of ArgoCD

# Installing Keptn with Kustomise
kubectl kustomize kube-infra/kustomize/keptn/base --enable-helm
kubectl apply -k kube-infra/kustomize/keptn/overlays/demo

# SSO
I am using Azure for SSO.  There is a secret called 

# Sealed Secrets
BASE64 ENCODE AWS KEY AND SECRETS

kubeseal <mysecret.json >mysealedsecret.json

kubeseal <aws-dns-creds-secret-argo-cd.yaml >aws-dns-creds-secret-argo-cd.enc.json --controller-namespace kube-secrets

apiVersion: v1
kind: Secret
metadata: name: aws-dns-creds
namespace: kube-infra
type: Opaque
data:
  AWS_ACCESS_KEY: 
  AWS_SECRET_ACCESS_KEY: 

