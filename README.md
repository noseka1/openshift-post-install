# openshift-post-install

Find out if a resource defined in the `htpasswd-secret.yaml` manifest already exists in OpenShift:
```
oc get --filename htpasswd-secret.yaml
```

If the resource doesn't exist in OpenShift, create the resource using:
```
oc apply --filename htpasswd-secret.yaml
```
If you create a resource using `oc apply`, a `kubectl.kubernetes.io/last-applied-configuration` annotation is attached to the resource. This annotation holds the last configuration applied to the resource. Following updates to the resource via `oc apply` will perform a three-way diff between the previously applied configuration, the provided input and the current configuration of the resource. This three-way diff provides you with better control over resource modifications than a simple diff performed for example by the `oc patch` command.

# Cluster Logging

The following commands will deploy cluster logging components on OpenShift. See also the [Logging documentation](https://docs.openshift.com/container-platform/latest/logging/cluster-logging.html).

```
$ oc apply --kustomize logging/elasticsearch-operator/base
```
```
$ oc apply --kustomize logging/cluster-logging-operator/base
```
```
$ oc apply --kustomize logging/cluster-logging-instance/base
```