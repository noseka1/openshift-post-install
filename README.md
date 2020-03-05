# openshift-post-install

Find out if a resource defined in the `htpasswd-secret.yaml` manifest already exists in OpenShift:
```
oc get --filename htpasswd-secret.yaml
```

If the resource doesn't exist in OpenShift, create the resource using:
```
oc apply --filename htpasswd-secret.yaml
```

Resources created using `oc apply` can be updated using `oc apply`.
