---
title: Login to the Keycloak admin console
description: This tutorial explains how create login to the Keycloak admin console
---

### Login to the Keycloak admin console


Step 1: Before logging into the Admin Console, you need to check what is the Admin Username and Password. The credentials are stored inside the following Secret:


Execute below command to get the Credentials Secret:

```execute
kubectl get keycloak example-keycloak -n my-keycloak-operator --output="jsonpath={.status.credentialSecret}"
```


Output:

```
credential-example-keycloak
```

Step 2: Next, you need to know the username and password.

Execute below command to get Admin Username and Admin Password:

```execute
export ADMIN_USERNAME=$(kubectl get secrets credential-example-keycloak -n my-keycloak-operator --template='{{.data.ADMIN_USERNAME | base64decode }}') 
export ADMIN_PASSWORD=$(kubectl get secrets credential-example-keycloak -n my-keycloak-operator --template='{{.data.ADMIN_PASSWORD | base64decode }}') 
echo "Admin Username:$ADMIN_USERNAME" 
echo "Admin Password: $ADMIN_PASSWORD"
```


Step 3: Navigate to Keycloak URL using your browser and use Admin Username and Admin Password obtained in previous steps to login in keycloak Admin console.

Please refer below snapshot:


![](_images/login-using-creds.png)
