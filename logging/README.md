# Cluster Logging

The following commands will deploy cluster logging components on OpenShift. See also the [Logging documentation](https://docs.openshift.com/container-platform/latest/logging/cluster-logging.html).

## Deploy the standard EFK stack

```
$ oc apply --kustomize elasticsearch-operator/base
```

```
$ oc apply --kustomize cluster-logging-operator/base
```

To deploy cluster logging development purposes, run this command:

```
$ oc apply --kustomize cluster-logging-instance/overlays/development
```

To deploy cluster logging to production, run this command:

```
$ oc apply --kustomize cluster-logging-instance/overlays/production
```

To deploy cluster logging to only forward logs to the external fluentd/logstash:

```
$ oc apply --kustomize cluster-logging-instance/overlays/log-forwarding-only
```

## Deploy Event Router

Refer to [Working with Event Router](https://docs.openshift.com/container-platform/4.3/logging/cluster-logging-eventrouter.html) for more information.

```
$ oc process -f event-router/event-router-template.yaml | oc apply --filename -
```
