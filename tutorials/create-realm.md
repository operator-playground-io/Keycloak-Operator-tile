---
title: Keycloak Realm Creation
description: Learn how to create a Keycloak realm using Keycloak Admin console?
---


### What is a Realm?
 A realm in Keycloak is the equivalent of a tenant. The functionalities of a realm include the following: 
-	It allows you to create isolated groups of users and applications.
-	The default realm called master manages the Keycloak, but is not recommended for a user’s own applications.


### Create a Keycloak Realm.

Follow the steps below to create a Keycloak realm using Admin console.


**Step 1: Open the Keycloak Admin Console.**

**Step 2: Select the ‘master’ option from the dropdown by hovering the mouse on the menu.**
**Step 3: Click on `Add realm` option. See the snapshot below.**


  ![](_images/add-realm.png)

**Step 3: Fill in the form with the following values:

   Name: myrealm
   
   ![](_images/add-realm-form.png)
   
**Step 4: Fill in the form with the Name value as `myrealm`.**

**Step 5: Click on ‘Create’.**
   
![](_images/myrealm-created.png)


### Conclusion
You should be able to see the ‘myrealm’ Realm as shown above.
