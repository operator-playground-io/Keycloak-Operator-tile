---
title: Keycloak Instance Creation
description: Learn how to create Instance of your Keycloak Operator.
---

### Create Keycloak Instance 

The Keycloak custom resource YAML file contains three properties:

instances - controls the number of instances running in high availability mode.

externalAccess - if the enabled is `true`, the Operator creates a route for OpenShift or an Ingress for Kubernetes for the Keycloak cluster.

externalDatabase - applies only if you want to connect an externally hosted database. 

**Step 1: Create the below YAML File for Custom Resource of Keycloak Instance.**

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


**Step 2: Now execute below command to create a Keycloak instance.**

```execute
kubectl create -f keycloakInstance.yaml -n my-keycloak-operator
```

You should see the following resources being created.

```
keycloak.keycloak.org/example-keycloak created
```

Once it is successful, Keycloak will get started on Kubernetes.  This will also initially create an `admin` user with associated username and password.


**Step 3: Check the pods’ status.**

```execute
kubectl get pods -n my-keycloak-operator
```

You will see an output like the below.

```
NAME                                       READY   STATUS    RESTARTS   AGE
pod/keycloak-0                             1/1     Running   3          5m12s
pod/keycloak-operator-668cc5dc75-sdpdd     1/1     Running   0          8m2s
pod/keycloak-postgresql-85fcff4cdd-d485l   1/1     Running   5          5m12s
```

Please wait until pod STATUS is "Running", then proceed.


**Step 4: Check the progress of create process for all the Kubernetes resources.**

```execute
kubectl get all -n my-keycloak-operator
```


You will see an output like the below.

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



### Access Keycloak Admin Console

In this case Keycloak Operator creates an Ingress for Kubernetes for the Keycloak cluster.

In case the Ingress add-on is not enabled, Keycloak console can be accessed using NodePort Service. 


**Step 1: First, create the yaml definition for `NodePort` Service to access Keycloak Admin Console as below.**

```execute
cat <<'EOF' > keycloaknodeportsvc.yaml
apiVersion: v1
kind: Service
metadata:
  name: keycloak-svc
  labels:
    app: keycloak
spec:
  ports:
  - name: http
    port: 8443
    targetPort: 8443
    nodePort: 30524
  selector:
    app: keycloak
  type: NodePort
EOF
```

**Step 2: Execute the command below to create Keycloak `NodePort` Service.**

```execute
kubectl create -f keycloaknodeportsvc.yaml -n my-keycloak-operator
```

You will see an output like the below.

```
service/keycloak-svc created
```

Keycloak console can be accessed using NodePort Service via URL as below:

https://##DNS.ip##:30524/auth/admin 

You should be able to see a Keycloak login console as shown below

![](_images/login-page.png)


### Conclusion

We have created Keycloak Instance and able to access Keycloak login console. In further section, we will discuss the process of logging in to Keycloak admin Console as admin user.
