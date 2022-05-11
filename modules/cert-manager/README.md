
# Cert-Manager manifests

## Helm Repo

Run the following to add the appropriate chart repo to your Helm installation

```bash
helm repo add jetstack https://charts.jetstack.io
helm repo update
```

Use `jetstack/cert-manager` for the chart identifier

#### Chart version == 1.6.1

---

## Overview

In order to generate a compatible version of the manifests required to start a running `cert-manager` service, a donar Helm chart is used to render base manifests.
The manifests produced are then altered to work with the target envionrments using kustomise.
A `kustomization.yaml` file is created to provide the resource mainifesets expected to be included in an application.

---

### Generate the base manifests

Starting with generating the output of the following command:

```bash
helm template jetstack/cert-manager --set installCRDs=true > manifests.yaml
```

Breakdown the content of the manifests.yaml output into separate files that contain resource definitions for specific types.

+   crds (custom resource definitions)
+   webhooks (validating and mutating)
+   jobs (one off tasks)
+   sa (service accounts)
+   service (services)
+   ns (kubernetes namespace)

---

### Useful Links

+   <https://cert-manager.io/docs/installation/upgrading/remove-deprecated-apis/>
+   <https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definition-versioning/#upgrade-existing-objects-to-a-new-stored-version>
