# Traefik manifests

## Helm Repo

Run the following to add the appropriate chart repo to your Helm installation

```bash
helm repo add traefik https://helm.traefik.io/traefik
helm repo update
```

Use `traefik/traefik` for the chart identifier

### Chart version == 10.7.1

---

## Overview

In order to generate a compatible version of the manifests required to start a running `traefik` service, a donar Helm chart is used to render base manifests.
The manifests produced are then altered to work with the target envionrments using kustomise.
A `kustomization.yaml` file is created to provide the resource mainifesets expected to be included in an application.

---

### Generate the base manifests

Starting with generating the output of the following command:

```bash
helm template traefik/traefik --include-crds --version 10.7.1 > manifests.yaml
```

Breakdown the content of the manifests.yaml output into separate files that contain resource definitions for specific types.

+   crds (custom resource definitions)
+   webhooks (validating and mutating)
+   deployment
+   middleware
+   sa (service accounts)
+   service (services)

The traefik resources are deployed into the `kube-system` namespace so an additional namespace is not required.
We also use a pod-disruption-budget to minimise the number of unavailable pods during an upgrade or service interruption.

---

### Useful Links

+   <https://doc.traefik.io/traefik/getting-started/install-traefik/>
