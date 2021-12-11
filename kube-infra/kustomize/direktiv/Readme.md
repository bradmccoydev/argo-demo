# Installation
kubectl apply -k kube-infra/kustomize/direktiv/overlays/demo --enable-helm

kube-infra/kustomize/direktiv/overlays/demo/kustomization.yaml

kubetcl create ns direktiv-services-direktiv

helm repo add direktiv https://charts.direktiv.io
helm install knative direktiv/knative

helm install -n direktiv --create-namespace direktiv direktiv/direktiv 


for ns in "default" "postgres" "knative-serving" "direktiv-services-direktiv"
do
  kubectl create namespace $ns || true
  kubectl annotate ns --overwrite=true $ns linkerd.io/inject=enabled
done;

NAME                    CHART VERSION   APP VERSION     DESCRIPTION                
direktiv/direktiv       0.5.10          v0.5.10         direktiv helm chart        
direktiv/knative        0.5.10          v0.5.10         knative for direktiv       
direktiv/pgo            0.5.10          v0.5.10         A Helm chart for Kubernetes