---
title: Keycloak Realm Role Creation
description: Learn how to create a Keycloak realm Roles using Keycloak Admin console.
---

### Create Realm Roles

Applications often assign access and permissions to specific roles rather than individual users as dealing with users can be too fine grained and hard to manage.

Let’s create "app-user" and "app-admin" Realm roles by assigning corresponding Client Roles: user, admin.

1. Click on the Roles menu from the left pane. All the available roles for the selected Realm will get listed here.

2. To create "app-user" realm role, click Add Role. You will be prompted for a Role Name, and a Description. Provide the details as below and Save.

3. Enabled Composite Roles and Search for `vanilla` under Client Roles field. Select user role of the `vanilla` client and Click Add Selected .

This configuration will assign `vanilla` client role : `user` to the `app-user` realm role.

4. Follow the same steps to create the app-admin realm role and assign `vanilla` client role : `admin` to it.
