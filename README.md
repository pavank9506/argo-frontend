
# argo-frontend

This repository provides a sample Kubernetes GitOps setup, suitable for use with Argo CD. It demonstrates a modular approach to managing applications, namespaces, and network policies using both Kustomize and Helm.

## Repository Structure

```
argo-frontend/
├── app-of-apps.yaml              # Argo CD App of Apps manifest
├── applications/                 # Kustomize manifests for Argo CD Applications
│   ├── frontend.yaml
│   ├── namespaces.yaml
│   └── network-policies.yaml
├── frontend/                     # Helm chart for the frontend application
│   ├── application.yaml          # Argo CD Application manifest for frontend
│   ├── Chart.yaml                # Helm chart metadata
│   ├── values.yaml               # Helm values
│   └── templates/                # Helm templates
│       ├── config-map.yaml
│       ├── deployment.yaml
│       ├── hpa.yaml
│       └── service.yaml
├── namespaces/                   # Namespace definitions
│   └── firstnamespace.yaml
├── network-policies/             # Network policy manifests
│   └── backend-frontend.yaml
└── README.md
```

## Key Components

- **app-of-apps.yaml**: The entrypoint manifest for Argo CD, which manages all other applications as children.
- **applications/**: Contains Kustomize manifests to define Argo CD Applications for different components (frontend, namespaces, network policies).
- **frontend/**: A Helm chart for deploying the frontend application, including deployment, service, config map, and HPA templates.
- **namespaces/**: Namespace YAML definitions for the cluster.
- **network-policies/**: NetworkPolicy resources to control traffic between components.

## Usage

1. **App of Apps Pattern**: Apply `app-of-apps.yaml` to your Argo CD instance to bootstrap all applications.
2. **Helm Chart**: The `frontend` directory is a Helm chart. You can deploy it directly with Helm or let Argo CD manage it as a Helm application.
3. **Kustomize Applications**: The `applications` directory contains Kustomize manifests for Argo CD Applications, which reference the Helm chart and other resources.

## Example: Deploying with Argo CD

1. Add this repository to Argo CD as a Git source.
2. Create an Argo CD Application using `app-of-apps.yaml`:
	```sh
	kubectl apply -f app-of-apps.yaml
	```
3. Argo CD will recursively create and manage all child applications defined in the `applications/` directory.

## Customization

- Modify the Helm values in `frontend/values.yaml` to customize the frontend deployment.
- Add or update network policies in `network-policies/` as needed.
- Add new namespaces in `namespaces/`.

## License

MIT
