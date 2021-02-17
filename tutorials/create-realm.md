---
title: Create Keycloak Realm using Keycloak Admin Console
description: This tutorial explains how to create Keycloak Realm using Keycloak Admin Console
---


### Create a realm

 Realm in Keycloak is the equivalent of a tenant. It allows creating isolated groups of applications and users. 
 By default there is a single realm in Keycloak called master. 
 This is dedicated to manage Keycloak and should not be used for your own applications.

Please follow following Steps to create Keycloak Realm using Keycloak Admin Console :

1. Open the Keycloak Admin Console.

2. Hover the mouse over the dropdown in the top-left corner where it says Master, then click on Add realm.Please refer following snapshot:

  ![](_images/add-realm.png)

3. Fill in the form with the following values:

   Name: myrealm
   
   ![](_images/add-realm-form.png)
   
4. Click on Create.

5. You will see Realm with name myrealm created as follows:
   
   ![](_images/myrealm-created.png)
