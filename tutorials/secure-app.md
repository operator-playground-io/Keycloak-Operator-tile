---
title: Create Client and configure it 
description: Learn how to create Client and configure it to register application with keycloak instance.
---


### Create Client and configure it 


Register the Application with Keycloak Instance by following steps below.


**Step 1: Open the Keycloak Admin Console.**

**Step 2: Click on 'Clients'.**

![](_images/create-client.png)

**Step 3: Fill up the form with the following values:**

   **Client ID: myclient  
   Client Protocol: openid-connect
   Root URL: https://www.keycloak.org/app/**
   
![](_images/client-config.png)

**Step 4: Click `Save`.**

 ![](_images/client-config.png)
   
   
### Secure the Application

**Step 1: Open https://www.keycloak.org/app/.**

You will see information following on console:

 
![](_images/account-console-new.png)
   
**Step 2: Change Keycloak URL to the URL of your Keycloak instance, i.e.**

https://##DNS.ip##:30524/auth/

![](_images/account-console-url-add.png)

**Step 3: Click on Save.**

**Step 4: Click on `Sign in` to authenticate to the application using the Keycloak server you started earlier.**

![](_images/account-console-signin.png)

After logging in, you will see a welcome message for the logged-in user on the console.

![](_images/login-application.png)


### Conclusion

Now you have created Client and configure it to register the sample application with Keycloak Instance.
