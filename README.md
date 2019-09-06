# kustomize

* tool for customizing k8s configurations
* included in `kubectl` >= 1.14
* similar to Docker layers

## Basic workflow

```
# create base manifests
mkdir k8s/base -p
vi k8s/base/service.yaml
vi k8s/base/deploy.yaml
vi k8s/base/kustomization.yaml

# add overlays to base
mkdir k8s/overlays/prod -p
vi k8s/overlays/prod/custom-env.yaml
vi k8s/overlays/prod/kustomization.yaml
```

## Basic commands

```
# view resources
kubectl kustomize k8s/base
kubectl kustomize k8s/overlays/prod

# apply resource:
kubectl apply -k k8s/base
kubectl apply -k k8s/overlays/prod

# delete resource:
kubectl delete -k k8s/base
kubectl delete -k k8s/overlays/prod
```

## Generating resources

configMapGenerator:

```
vi k8s/overlays/prod/application.properties
vi k8s/overlays/prod/kustomization.yaml # configMapGenerator
```

secretGenerator

```
vi k8s/overlays/prod/password.txt
vi k8s/overlays/prod/kustomization.yaml # secretGenerator
```

## Cross-cutting fields

You can add fields into kustomization.yaml that will be applied to all resources, e.g.:

```
namespace: my-namespace
namePrefix: dev-
nameSuffix: "-001"
commonLabels:
  project: manhattan
commonAnnotations:
  oncallPager: 800-555-1212
resources:
- deployment.yaml
```

## Resources:

* https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/
* https://blog.stack-labs.com/code/kustomize-101/
* https://kubectl.docs.kubernetes.io/pages/reference/kustomize.html