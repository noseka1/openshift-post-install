# openshift-post-install

Find out if a resource defined in the `<name>.yaml` manifest already exists in OpenShift:

```
$ oc get --filename <name>.yaml
```

## Using oc apply

You can create or modify a resource in OpenShift using an `oc apply` command:
```
$ oc apply --filename <name>.yaml
```
If you create or modify a resource using `oc apply`, a `kubectl.kubernetes.io/last-applied-configuration` annotation will be attached to the resource. This annotation holds the last configuration applied to the resource. Following updates to the resource via `oc apply` will perform a three-way diff between the previously applied configuration, the provided input and the current configuration of the resource. This three-way diff provides you with a better control over resource modifications than a simple diff performed by the `oc patch` command. Future changes to the resource should be based off the last applied input file, i.e. you modify the last applied input file to fit your needs and reapply it.

## Using oc patch

Existing resources can be modified using an `oc patch` command:

```
$ oc patch --filename <name>.yaml --patch "$(cat <name>.yaml)"
```

Resources that don't support strategic-mege patch can be patched this way:

```
$ oc patch --filename <name>.yaml --patch "$(cat <name>.yaml)" --type merge
```

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
