---
title: Keycloak Instance Creation tutorial
description: This tutorial explains how create Instances for your Keycloak Operator.
---

### Create Keycloak Instance 
The Keycloak custom resource YAML file contains three properties:

instances - controls the number of instances running in high availability mode.

externalAccess - if the enabled is True, the Operator creates a route for OpenShift or an Ingress for Kubernetes for the Keycloak cluster.

externalDatabase - applies only if you want to connect an externally hosted database. 

### Create below yaml to create CR for Keycloak Instance

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


Execute below command to create Keycloak instance:

```execute
kubectl create -f keycloakInstance.yaml -n my-keycloak-operator
```

You will see the following resources created:

```
keycloak.keycloak.org/example-keycloak created
```

This will start Keycloak on Kubernetes. It will also create an initial admin user with username and password.


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

Please wait till Pod STATUS will be "Running" and then proceed further.


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


- Create below yaml for NodePort service to access Keycloak Admin Console:


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

- Execute below command to create Keycloak NodePort Service:

```execute
kubectl create -f nodeportsvc.yaml -n my-keycloak-operator
```

Output:

```
service/keycloak-svc created
```

### Access Keycloak Admin Console

In this case Keycloak Operator creates an Ingress for Kubernetes for the Keycloak cluster.

If we don’t have the Ingress addon enabled,we can access Keycloak using NodePort from the following URL:

<a href="https://##DNS.ip##:30524/auth/admin" target="_blank">https://##DNS.ip##:30524/auth/admin</a> 


### Login to the Keycloak admin console
Before logging into the Admin Console, you need to check what is the Admin Username and Password. The credentials are stored inside the following Secret:


Execute below command to get the Credentials Secret:

```execute
kubectl get keycloak example-keycloak --output="jsonpath={.status.credentialSecret}"
```


Output:

```
credential-example-keycloak
```

Next, you need to view the username and password:

```execute
ADMIN_USERNAME=kubectl get secrets credential-example-keycloak -n my-keycloak-operator --template='{{.data.ADMIN_USERNAME | base64decode }}' &&
echo "" &&
ADMIN_PASSWORD=kubectl get secrets credential-example-keycloak -n my-keycloak-operator --template='{{.data.ADMIN_PASSWORD | base64decode }}' &&
echo "" &&
echo "Admin Username:                 $ADMIN_USERNAME" &&
echo "Admin Password:   $ADMIN_PASSWORD" 
```


Navigate to Keycloak URL using your browser and use Admin Username and Admin Password obtained in previous steps to login in keycloak Admin console.

