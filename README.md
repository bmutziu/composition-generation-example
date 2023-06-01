# composition-generation-example

this project uses https://github.com/crossplane-contrib/x-generation as base.

```bash
make generate
```

to build configuration package you can use:

```bash
cd compositions
find . -name \generate.yaml -type f -delete
kubectl crossplane build configuration --name compositions
kubectl crossplane push configuration ${CI_REGISTRY_IMAGE}/compositions:${IMAGE_TAG}
kubectl crossplane push configuration ${REGISTRY_URL}:${IMAGE_TAG}
```

to use the configuration package you can use:

```bash
---
apiVersion: pkg.crossplane.io/v1
kind: Configuration
metadata:
  name: compositions
spec:
  package: ${CI_REGISTRY_IMAGE}/compositions:${IMAGE_TAG}
  commonLabels:
    version: ${IMAGE_TAG}
```