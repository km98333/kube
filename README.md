# Static web with letsencrypt ssl and kubernetes

## Environment

Local kubernetes cluster

## Plan

- Metallb as a load balancer for bare metal
- Static website working on nginx container with configuration mounted as config map and website as volume mount.
- Nginx Ingress for http traffic and SSL control
- Cert-Manager to support letsencrypt certificates

## Installation

For this purpose i used NGINX Ingress and Cert-Manager

Metallb
```bash
kubectl apply -f https://raw.githubusercontent.com/google/metallb/v0.7.3/manifests/metallb.yaml
```

NGINX Ingress
```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/mandatory.yaml
```

Cert-Manager

```bash
kubectl create namespace cert-manager
kubectl label namespace cert-manager certmanager.k8s.io/disable-validation=true
kubectl apply -f https://github.com/jetstack/cert-manager/releases/download/v0.8.0-beta.0/cert-manager.yaml
```
## Manifests

```bash
kubectl apply -f staticweb-svc.yaml
kubectl apply -f staticweb-cm.yaml
kubectl apply -f staticweb-deploy.yaml
kubectl apply -f letsencrypt_issuer.yaml
kubectl apply -f ingress-svc.yaml
kubectl apply -f ingress-deploy.yaml
```
