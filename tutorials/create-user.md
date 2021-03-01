---
title: User Creation using Keycloak Admin Console
description: Learn how to create user using Keycloak Admin Console.
---


### Create a user

Initially, there is no existing user in the new realm. Let’s create one using Keycloak admin console. To do so, follow the steps below.  


**Step 1: Open the Keycloak Admin Console and click on Users menu.**

Step 2: Click on ‘Add User’ on the top right corner.

 ![](_images/users-option.png)

Step 3: Fill up the form with following field values:

   Username: myuser
   First Name: John
   Last Name: Rodger


 ![](_images/add-user.png)
 

Step 4: Click on `Save`.

 ![](_images/add-user-form.png)

### Create Password

After defining the user account details, you will need an initial password to be created. To do so,

Step 1: Click on the Credentials.

 ![](_images/user-creds.png)

Step 2: Enter the password in Set Password field. 

 ![](_images/enter-user-password.png)

3. Select "ON" next to "Temporary" which will make it "OFF" to prevent the user being prompted to update the password at first. login. 

![](_images/ON-option.png)

You should see the details on console like below.

 ![](_images/set-password.png)
 
Please provide your confirmation by clicking on "Set Password" again.

### Conclusion

User with its username and password is created.
