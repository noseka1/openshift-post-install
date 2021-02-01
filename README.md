# Configuration settings to be applied after OpenShift installation

Find out if a resource defined in the `<name>.yaml` manifest already exists in OpenShift:

```
$ oc get --filename <name>.yaml
```

## Using oc apply

You can create or modify a resource in OpenShift using an `oc apply` command:
```
$ oc apply --filename <name>.yaml
```
If you create or modify a resource using `oc apply`, a `kubectl.kubernetes.io/last-applied-configuration` annotation will be attached to the resource. This annotation holds the last configuration applied to the resource. Following updates to the resource via `oc apply` will perform a three-way merge based upon the previously applied configuration, the provided input and the current configuration of the resource. This three-way merge provides you with a better control over resource modifications than a simple patch performed by an `oc patch` command. There is one caveat when using `oc apply` though: **future changes to the same resource should be based off the last applied input file, i.e. you modify the last applied input file to fit your needs and reapply it.** Otherwise you would be running into a danger of dropping the previously applied configuration.

## Using oc patch

Existing resources can be modified using an `oc patch` command (defaults to *strategic* patch type):

```
$ oc patch --filename <name>.yaml --patch "$(cat <name>.yaml)"
```

Resources that don't support strategic-mege patch can be patched this way:

```
$ oc patch --filename <name>.yaml --patch "$(cat <name>.yaml)" --type merge
```
