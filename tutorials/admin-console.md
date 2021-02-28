---
title:Login to the Keycloak admin console
description: Learn how to log in to Keycloak admin console using credentials.
---

### Login to the Keycloak admin console

Before logging into the admin console, you need to check the admin user credentials, i.e. username and password for the admin account. These credentials are stored a particular Secret.


**Step 1: Execute below command to get the Secret.**


```execute
kubectl get keycloak example-keycloak -n my-keycloak-operator --output="jsonpath={.status.credentialSecret}"
```

This should produce the following output.

```
credential-example-keycloak
```

Next, you need to know the username and password.

**Step 2: Execute the command below to get username and password for Admin account.**

```execute
export ADMIN_USERNAME=$(kubectl get secrets credential-example-keycloak -n my-keycloak-operator --template='{{.data.ADMIN_USERNAME | base64decode }}') 
export ADMIN_PASSWORD=$(kubectl get secrets credential-example-keycloak -n my-keycloak-operator --template='{{.data.ADMIN_PASSWORD | base64decode }}') 
echo "Admin Username:$ADMIN_USERNAME" 
echo "Admin Password: $ADMIN_PASSWORD"
```


Step 3: Navigate to Keycloak URL using your browser and log in to Keycloak Admin console using the credentials retrieved in the previous step.

See the snapshot below.


![](_images/login-using-creds.png)

### Conclusion

You’re done. Now you can access and manage tasks relevant to Admin user account.
