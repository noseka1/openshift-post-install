To enable the log-forwarding Tech Preview feature, set the annotation on the ClusterLogging resource:

```
apiVersion: logging.openshift.io/v1
kind: ClusterLogging
metadata:
  annotations:
    clusterlogging.openshift.io/logforwardingtechpreview: enabled
  name: instance
  namespace: openshift-logging
  
  ...
```
