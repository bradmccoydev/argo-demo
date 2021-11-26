![GitHub](https://img.shields.io/github/license/bradmccoydev/argo-demo)
# Argo Demo
This Repo is for a Demo of ArgoCD

# Configuration / Installation of ArgoCD

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

