# Create a sample-trust.crt, and sample-trust.key

Install step with
``` brew install step ```

step certificate create root.linkerd.cluster.local sample-trust.crt sample-trust.key \
  --profile root-ca \
  --no-password \
  --not-after 43800h \
  --insecure

step certificate inspect sample-trust.crt

```
kubectl -n linkerd create secret tls linkerd-trust-anchor \
  --cert sample-trust.crt \
  --key sample-trust.key \
  --dry-run=client -oyaml | \

kubeseal --controller-name=sealed-secrets -oyaml - | \

kubectl patch -f - \
  -p '{"spec": {"template": {"type":"kubernetes.io/tls", "metadata": {"labels": {"linkerd.io/control-plane-component":"identity", "linkerd.io/control-plane-ns":"linkerd"}, "annotations": {"linkerd.io/created-by":"linkerd/cli stable-2.8.1", "linkerd.io/identity-issuer-expiry":"2021-07-19T20:51:01Z"}}}}}' \
  --dry-run=client \
  --type=merge \
  --local -oyaml > gitops/resources/linkerd/trust-anchor.yaml
```

exp=$(date -v+8760H +"%Y-%m-%dT%H:%M:%SZ") && echo $exp

helm install linkerd2 \
  --set-file identityTrustAnchorsPEM=ca.crt \
  --set-file identity.issuer.tls.crtPEM=issuer.crt \
  --set-file identity.issuer.tls.keyPEM=issuer.key \
  --set identity.issuer.crtExpiry=$exp \
  -f linkerd2/values-ha.yaml \
  linkerd/linkerd2

  kustomize build kube-infra/kustomize/direktiv/direktiv-postgres/overlays/demo --enable-helm | kubectl -f

  kustomize build kube-infra/kustomize/service-mesh/linkerd/overlays/demo --enable-helm

sample-trust.crt
sample-trust.key