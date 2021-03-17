---
title: Create Client and configure it 
description: Learn how to create Client and configure it.
---


### Create Client and configure it 


Create Client and configure it by following steps below.


**Step 1: Open the Keycloak Admin Console.**

**Step 2: Click on 'Clients' and then on `Create`**

![](_images/create-client.png)

**Step 3: Fill up the form with the following values:**

   Client ID: vanilla  
   
   Client Protocol: openid-connect
   
   Root URL: http://##DNS.ip##:30300
   
![](_images/client-form.png)

**Step 4: Click `Save`.**

You will see Client `Settings` information like below: 

![](_images/client-setting-page.png)
    
   
### Define Client Roles

Imagine the Application that you are building, have different types of users with different user permissions. Ex: users and administrators.

- Some APIs would only be accessible to `users` only.

- Some APIs would be accessible to `administrators` only.

- Some APIs would be accessible to both `users` and `administrators`.

**Step 1: Go to Client `Roles` tab. Click on `Add-Role` to create the Client Role definitions.**

You will see following on console:
 
![](_images/add-role-to-client.png)
   
**Step 2: Let’s create two roles: user and admin by clicking Add Role button.**

- Provide the Role Name: user. Click on `Save`

![](_images/add-role-user.png)

- Provide the other Role Name: admin. Click on `Save`

![](_images/add-role-admin.png)



### Conclusion

Now you have created Client and configure it.
