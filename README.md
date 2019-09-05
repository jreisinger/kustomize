## kustomize

* included in `kubectl` >= 1.14
* similar to Docker layers

Workflow:

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

view resources:

```
kubectl kustomize k8s/base
kubectl kustomize k8s/overlays/prod
```

apply resource:

```
kubectl apply -k k8s/base
kubectl apply -k k8s/overlays/prod
```

Resources:

* https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/
* https://blog.stack-labs.com/code/kustomize-101/
* https://www.exoscale.com/syslog/kubernetes-kustomize/
