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
Keycloakinstance.Keycloakcontroller.min.io/Keycloak created
```

Check the Pods status:

```execute
kubectl get pods -n my-Keycloak-operator
```

You will see similar to this output:

```
NAME                              READY   STATUS    RESTARTS   AGE
Keycloak-0                           1/1     Running   0          115s
Keycloak-1                           1/1     Running   0          115s
Keycloak-2                           1/1     Running   0          115s
Keycloak-3                           1/1     Running   0          115s
Keycloak-operator-6cccf9f587-72xcp   1/1     Running   0          17m
```

Check all the kubernetes resources:

```execute
kubectl get all -n my-Keycloak-operator
```


You will see similar to this output:

```
NAME                                  READY   STATUS    RESTARTS   AGE
pod/Keycloak-0                           1/1     Running   0          2m8s
pod/Keycloak-1                           1/1     Running   0          2m8s
pod/Keycloak-2                           1/1     Running   0          2m8s
pod/Keycloak-3                           1/1     Running   0          2m8s
pod/Keycloak-operator-6cccf9f587-72xcp   1/1     Running   0          17m

NAME                   TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)    AGE
service/Keycloak-hl-svc   ClusterIP   None         <none>        9000/TCP   2m8s

NAME                             READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/Keycloak-operator   1/1     1            1           17m

NAME                                        DESIRED   CURRENT   READY   AGE
replicaset.apps/Keycloak-operator-6cccf9f587   1         1         1       17m

NAME                     READY   AGE
statefulset.apps/Keycloak   4/4     2m8s

```

### Create NodePort Service to access Keycloak's Pod 

```execute
cat <<'EOF' > KeycloakNodePortService.yaml
apiVersion: v1
kind: Service
metadata:
  name: Keycloak-service
spec:
  type: NodePort
  ports:
  - port: 9000
    nodePort: 30205
  selector:
    v1beta1.min.io/instance: Keycloak
EOF
```

Execute below command to create NodePort Service

```execute
kubectl create -f KeycloakNodePortService.yaml -n my-Keycloak-operator
```

Output:

```
service/Keycloak-service created
```

### Access Keycloak's dashboard

Execute below command to get the NodePort service:

```execute
kubectl get svc -n my-Keycloak-operator
```

Output will be similar to below output:

```
NAME            TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
Keycloak-hl-svc    ClusterIP   None            <none>        9000/TCP         84m
Keycloak-service   NodePort    10.107.138.82   <none>        9000:30205/TCP   81m
```

The Port value for "Keycloak-service" of Type NodePort is : 30205

We will use this port to access Keycloak's Pod using below URL: 

Click on http://##DNS.ip##:30205 to access Keycloak's dashboard from your browser.

You will see the Keycloak's Login page as below :


 ![](_images/login-console.PNG)



