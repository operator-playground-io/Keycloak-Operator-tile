---
title: Create User Tutorial using Keycloak Admin Console
description: This tutorial explains how to create user using Keycloak Admin Console
---


### Create a user

Initially there are no users in a new realm, so let’s create one.

Follow below steps to create Users using Keycloak admin console:

Steps:

1. Open the Keycloak Admin Console.

2. Click Users (left-hand menu).

 ![](_images/users-option.png)

3. Click Add user (top-right corner of table).

 ![](_images/add-user.png)
 

4. Fill in the form with the following values:

   Username: myuser
   
   First Name: John
   
   Last Name: Rodger

5. Click Save.

 ![](_images/add-user-form.png)


The user will need an initial password set to be able to login. To do this:

1. Click Credentials (top of the page).

 ![](_images/user-creds.png)

2. Fill in the Set Password form with a password.

 ![](_images/enter-user-password.png)

3. Click ON next to Temporary to prevent having to update password on first login.

![](_images/On-option.png)

4. You will see the similar to the below snapshot on console:

 ![](_images/set-password.png)
