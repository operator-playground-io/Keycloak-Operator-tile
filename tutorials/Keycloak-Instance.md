---
title: Keycloak Instance Creation tutorial
description: This tutorial explains how create Instances for your Keycloak Operator.
---

### Create Keycloak Instance 


### Create below yaml file to create Keycloak Operator Instance

```execute
cat <<'EOF' > keycloakInstance.yaml
apiVersion: keycloak.org/v1alpha1
kind: Keycloak
metadata:
  name: example-keycloak
  labels:
    app: sso
spec:
  instances: 1
  extensions:
    - >-
      https://github.com/aerogear/keycloak-metrics-spi/releases/download/1.0.4/keycloak-metrics-spi-1.0.4.jar
  externalAccess:
    enabled: true
EOF
```

Execute below command to create Keycloak Operator instance:

```execute
kubectl create -f keycloakInstance.yaml -n my-keycloak-operator
```

You will see the following output:

```
keycloak.keycloak.org/example-keycloak created
```

Check the Pods status:

```execute
kubectl get pods -n my-keycloak-operator
```

You will see similar to this output:

```
NAME                                       READY   STATUS    RESTARTS   AGE
pod/keycloak-0                             1/1     Running   3          5m12s
pod/keycloak-operator-668cc5dc75-sdpdd     1/1     Running   0          8m2s
pod/keycloak-postgresql-85fcff4cdd-d485l   1/1     Running   5          5m12s
```

Check all the kubernetes resources:

```execute
kubectl get all -n my-keycloak-operator
```


You will see similar to this output:

```
NAME                                       READY   STATUS    RESTARTS   AGE
pod/keycloak-0                             1/1     Running   3          5m12s
pod/keycloak-operator-668cc5dc75-sdpdd     1/1     Running   0          8m2s
pod/keycloak-postgresql-85fcff4cdd-d485l   1/1     Running   5          5m12s

NAME                                TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)             AGE
service/keycloak                    ClusterIP   10.96.176.239    <none>        8443/TCP            5m12s
service/keycloak-discovery          ClusterIP   None             <none>        8080/TCP            5m12s
service/keycloak-operator-metrics   ClusterIP   10.109.132.56    <none>        8383/TCP,8686/TCP   7m53s
service/keycloak-postgresql         ClusterIP   10.109.139.250   <none>        5432/TCP            5m12s

NAME                                  READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/keycloak-operator     1/1     1            1           8m2s
deployment.apps/keycloak-postgresql   1/1     1            1           5m12s

NAME                                             DESIRED   CURRENT   READY   AGE
replicaset.apps/keycloak-operator-668cc5dc75     1         1         1       8m2s
replicaset.apps/keycloak-postgresql-85fcff4cdd   1         1         1       5m12s

NAME                        READY   AGE
statefulset.apps/keycloak   1/1     5m12s
```

