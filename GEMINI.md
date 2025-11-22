# GEMINI.md

## Project Overview

This project contains the Kubernetes manifests to deploy AdGuard Home. It uses a `kustomize` setup with a `base` and an `overlays/dev` directory.

The `base` directory contains the core manifests for the AdGuard Home deployment, including:
*   `adguard-home-deployment.yaml`: A Deployment to run the AdGuard Home application.
*   `adguard-home-service.yaml`: A ClusterIP Service to expose the AdGuard Home web interface and DNS servers within the cluster.
*   `adguard-home-ingress-local.yaml`: An Ingress to expose the AdGuard Home web interface outside the cluster.
*   `adguard-home-pv-pvc.yaml`: A PersistentVolumeClaim to provide persistent storage for AdGuard Home data.
*   `namespace.yaml`: A Namespace to isolate the AdGuard Home resources.
*   `service-account.yaml`: A ServiceAccount for the AdGuard Home pod.

The `overlays/dev` directory contains a patch to update the image tag for the AdGuard Home container.

## Building and Running

To deploy the application using the `dev` overlay, run the following command:

```bash
kubectl apply -k overlays/dev
```

To deploy the base configuration without the development overlay, use:

```bash
kubectl apply -k base
```

## Development Conventions

The project follows the standard `kustomize` convention of using a `base` for common resources and `overlays` for environment-specific configurations. The `dev` overlay is used for development and it patches the image of the AdGuard Home container. This is a common pattern to manage different configurations for different environments (e.g., development, staging, production).
