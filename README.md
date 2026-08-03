# kubernetes-course-bootdev

Kubernetes manifests for deploying the Boot.dev SynergyChat sample application.

## What is in this repository

- **API**: deployment, service, config map, persistent volume claim, and HTTP route
- **Web**: deployment, service, config map, HTTP route, and HPA
- **Crawler**: deployment, service, and config map (in the `crawler` namespace)
- **Gateway API**: `GatewayClass` and `Gateway`
- **Autoscaling/limits demos**: `testcpu-*` and `testram-*` manifests

## Prerequisites

- A running Kubernetes cluster
- Gateway API support in the cluster
- A Gateway controller that handles `gateway.envoyproxy.io/gatewayclass-controller`

## Quick start

1. Create the crawler namespace:

   ```bash
   kubectl create namespace crawler
   ```

2. Apply core manifests from the repository root:

   ```bash
   kubectl apply -f app-gatewayclass.yaml
   kubectl apply -f app-gateway.yaml

   kubectl apply -f crawler-configmap.yaml
   kubectl apply -f crawler-deployment.yaml
   kubectl apply -f crawler-service.yaml

   kubectl apply -f api-configmap.yaml
   kubectl apply -f api-pvc.yaml
   kubectl apply -f api-deployment.yaml
   kubectl apply -f api-service.yaml
   kubectl apply -f api-httproute.yaml

   kubectl apply -f web-configmap.yaml
   kubectl apply -f web-deployment.yaml
   kubectl apply -f web-service.yaml
   kubectl apply -f web-httproute.yaml
   kubectl apply -f web-hpa.yaml
   ```

3. (Optional) Apply the autoscaling/resource test manifests:

   ```bash
   kubectl apply -f testcpu-deployment.yaml
   kubectl apply -f testcpu-hpa.yaml
   kubectl apply -f testram-configmap.yaml
   kubectl apply -f testram-deployment.yaml
   ```

## Notes

- The web route uses host `synchat.internal`.
- The API route uses host `synchatapi.internal`.
- The web app calls the API via `http://synchatapi.internal`.
