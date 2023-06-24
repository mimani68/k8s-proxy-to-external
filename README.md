
# Kubernetes Proxy request to external resource

## Ingress installation

```bash
helm upgrade --install ingress-nginx ingress-nginx \
    --repo https://kubernetes.github.io/ingress-nginx  \
    --namespace ingress-nginx \
    --create-namespace \
    --set defaultBackend.image.registry=docker.iranrepo.ir \
    --set controller.image.registry=docker.iranrepo.ir \
    --set controller.admissionWebhooks.patch.image.registry=docker.iranrepo.ir
```

## Installing proxy k8s manifests

```bash
kubectl apply -f ingress.yaml -f external.service.yaml
```

## Test functionality

```bash
curl --header 'Host: mockbin.org' http://<server-ip>:<server-port>/request?code=12
```