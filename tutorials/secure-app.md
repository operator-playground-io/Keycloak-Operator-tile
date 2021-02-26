---
title: Secure our first application using Keycloak Admin Console
description: This tutorial explains how to secure our first application using Keycloak Admin Console
---


### Secure our first application


First step is to register this application with your Keycloak instance. To do this follow below steps:


1. Open the Keycloak Admin Console.

2. Click on 'Clients' and then click on the option "Create" as shown in below snapshot.

   ![](_images/create-client.png)

3. Fill in the form with the following values:

   Client ID: myclient
  
   Client Protocol: openid-connect
  
   Root URL: https://www.keycloak.org/app/
   
   ![](_images/client-config.png)

4. Click Save.

   ![](_images/client-config.png)

5. Open https://www.keycloak.org/app/. You will see following on console:
 
   ![](_images/account-console-new.png)
   
6. Change Keycloak URL to the URL of your Keycloak instance : https://##DNS.ip##:30524/auth/.

    ![](_images/account-console-url-add.png)

7. Click Save.

8. Now you can click Sign in to authenticate to this application using the Keycloak server you started earlier.

  ![](_images/account-console-signin.png)

  You will see a welcome message for the logged-in user on console.

  ![](_images/login-application.png)


