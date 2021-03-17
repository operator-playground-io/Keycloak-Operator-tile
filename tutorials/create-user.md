---
title: User Creation using Keycloak Admin Console
description: Learn how to create user using Keycloak Admin Console.
---


### Create a user

Initially, there is no existing user in the new realm. Let’s create one using Keycloak admin console. To do so, follow the steps below.  


**Step 1: Open the Keycloak Admin Console and click on Users menu.**

**Step 2: Click on ‘Add User’ on the top right corner.**

 ![](_images/users-option.png)

**Step 3: Fill up the form with following field values:

    Username: employee1
    
    First Name: John
    
    Last Name: Rodger


 ![](_images/add-user.PNG)
 

**Step 4: Click on `Save`.**


### Create Password

After defining the user account details, you will need an initial password to be created. To do so,

**Step 1: Click on the Credentials.**

 ![](_images/user-creds.png)

**Step 2: Enter the password in Set Password field.**

 ![](_images/enter-user-password.png)

**Step 3: Select "ON" next to "Temporary" which will make it "OFF" to prevent the user being prompted to update the password at first login.**

![](_images/ON-option.png)

You should see the details on console like below.

 ![](_images/set-password.png)
 
Please provide your confirmation by clicking on "Set Password" again.

### Role Mapping to Users

Step 1: Click the Role Mappings tab to assign realm roles to the user. 

Realm roles list will be available in Available Roles list. 

Step 2: Select one required role and click on the Add Selected > to assign it to the user.

![](_images/user-role-mapping.png)

After role assignment, assigned roles will be available under Assigned Roles list. 


Similarly Create users : employee2 and employee3. Set the credential for them by following above steps.


- Assign `app-admin` realm role to employee2 by following above steps.

![](_images/admin-role-mapping.png)

- Assign `app-user` and `app-admin` realm roles to employee3 by following above steps.

![](_images/both-role-mapping.png)

### Conclusion

User with its username and password with Role mapping is created.
