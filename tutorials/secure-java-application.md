---
title: Secure a Sample Application using Keycloak.
description: Learn how to use a Keycloak cluster to add authentication to an applications and secure the services.
---


### Introduction

The sample application we have considered here is a REST Java service application which is deployed as a microservice and it is protected by keycloak. The REST Service is accessed by a Node.js client application.
Any unauthenticated user will be able to access the Home page. The regular users will be able to access the 'Courses' page and the users with 'teacher' role will be able to remove courses.
The example also uses Skaffold tool which handles the workflow for building, pushing and deploying an application, allowing the developer to focus on writing the code.

### Code Structure

![codestructure](_images/keycloak-sample-app-structure.png)

The code stucture follows a simple modular and MVC pattern. There are 4 folders that are of our interest:
   - backend : This folder contains the sources for the REST Service Java Spring application.
   - frontend : This folder contains the sources for the Node.js frontend application.
	- k8s : This folder contains all the deployment and service yaml files for the application. This defines the deployment and exposure of our application.
	- k8s_keycloak : This folder contains all the deployment and service yaml files for creating an a Keycloak cluster if you need, for example to run the application locally.



### Try the example

**Step 1: Perform the following steps described in the tutorials.**

*  Install the Keycloak operator.

*  Create an Keycloak cluster.

*  Login to Keycloak Admin Console.

*  Create a realm with name 'university'.

*  Create a client with name 'course-management'. Use the following URL: http://##DNS.ip##:30690.

*  Make the following changes to 'course-management' client:
   - Access Type: Confidential
   - Service Accounts Enabled: True 
   - Authorization Enabled: True

   Click Save.

*  Click on Roles tab from the left menu and add 'teacher', 'ta', 'student' and 'parent' roles.

*  Create an user with username alen.tuning and password test1234. Assign the role teacher to it from 'Role mappings' tab. 
   Create an user with username rose.white and password test1234. Assign the role student to it from 'Role mappings' tab.
   
   Note: Please refer "Define Client Role" section of "Create Client and configure it" Tutorial and "Create Realm Roles" tutorial.

*  Define scopes for 'course-management' client. Open client and go to 'Authorization' tab and 'Authorization Scopes' tab. Click Create and set Name: view. Click Save.
   Create a new scope with Name: delete.

*  Define a resource for 'course-management' client. Go to 'Authorization' tab and 'Resources' tab. Click Create and set the following values:
   - Name: Course Resource
   - URI: /courses/*
   - Scopes: view and delete

*  Define policies for 'course-management' client. Go to 'Authorization' tab and 'Policies' tab. Click Create and Role and set the following values:
   - Name: only student policy
   - Roles: student

   Create 2 more policies with the following values:
   - Name: only ta policy, Roles: ta
   - Name: only teacher policy, Roles: teacher

*  Define permissions for 'course-management' client. Go to 'Authorization' tab and 'Permissions' tab. Click Create and Scope-Based and set the following values:
   - Name: View course permission
   - Scopes: view
   - Apply policy: 'only student policy', 'only ta policy' and 'only teacher policy'
   - Decision Strategy: Afirmative

   Create one more permission with the following values:
   - Name: Delete course permission
   - Scopes: delete
   - Apply policy: 'only teacher policy'
   - Decision Strategy: Afirmative


Once you complete the above steps, proceed with following steps to execute the sample application.

**Step 2: Install the sample application.**

- Get the sample code.

```execute
cd /home/student/projects && git clone https://github.com/operator-playground-io/keycloak-java-sample.git
```

- Navigate to the example.

```execute
cd keycloak-java-sample
```

- Set the Keycloak instance IP.

```execute
export ip_addr=$(ifconfig eth1 | grep inet | awk '{print $2}' | cut -f2 -d:)
```
```execute
sed -i "s/ip-address/$ip_addr/" ./frontend/.env
sed -i "s/ip-address/$ip_addr/" ./backend/src/main/resources/application.properties
```

Get the client secret from 'course-management' client page, Credentials tab, Secret field. Copy and run following commands replacing 1234 with the correct secret. The secret is something like ebd161d4-0117-4598-9d62-94e1711e95dd

sed -i "s/client-secret/1234/" ./frontend/.env

sed -i "s/client-secret/1234/" ./backend/src/main/resources/application.properties

- Setup skaffold default repository to the local one.
```execute
skaffold config set default-repo localhost:5000
```

- Install and start the sample application. 

```execute
skaffold run
```
Alternatively, you can use this command to install the sample, watch for code changes and re-deploy the application automatically. 

On exiting the command, Skaffold will automatically stop and delete the sample application.

```execute
skaffold dev
```

### Access the application

- Click on the Key () icon on the dashboard and copy the value under the DNS section and IP field.

Follow the below URL: 

http://##DNS.ip##:30600

The frontend application offers the following endpoint to get an access token required to access the REST Service.

http://##DNS.ip##:30600/access

Method: POST

Parameters:
- user - the name of the user (for example rose.white)
- password - the user password (for example test1234)

The access token is in the following format:

{
    "token": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICIzZDdCUVFyVVhlUEFLSjRjRWY2TmZIVlNDUmxZdEVXb2FPNWtwUXN3MTBNIn0.eyJleHAiOjE2MTk1NDIwOTcsImlhdCI6MTYxOTU0MTc5NywianRpIjoiMWU1YTY3MjAtMzdmNy00YjA0LTk2ZWMtOTQyZjJkZGExMmNhIiwiaXNzIjoiaHR0cDovL2xvY2FsaG9zdDo4MDgwL2F1dGgvcmVhbG1zL3VuaXZlcnNpdHkiLCJhdWQiOiJhY2NvdW50Iiwic3ViIjoiOTYwYWQ5ZmQtMzg2ZS00NjY1LTljNmMtOTA4ZjgzNWRjMzk3IiwidHlwIjoiQmVhcmVyIiwiYXpwIjoiY291cnNlLW1hbmFnZW1lbnQiLCJzZXNzaW9uX3N0YXRlIjoiNzNkZmE4ODgtNzAxMC00ZmE0LWJiOGYtZjcxOWFhZWNmODdlIiwiYWNyIjoiMSIsImFsbG93ZWQtb3JpZ2lucyI6WyJodHRwOi8vbG9jYWxob3N0OjgwOTAiXSwicmVhbG1fYWNjZXNzIjp7InJvbGVzIjpbInRlYWNoZXIiLCJvZmZsaW5lX2FjY2VzcyIsInVtYV9hdXRob3JpemF0aW9uIl19LCJyZXNvdXJjZV9hY2Nlc3MiOnsiYWNjb3VudCI6eyJyb2xlcyI6WyJtYW5hZ2UtYWNjb3VudCIsIm1hbmFnZS1hY2NvdW50LWxpbmtzIiwidmlldy1wcm9maWxlIl19fSwic2NvcGUiOiJvcGVuaWQgcHJvZmlsZSBlbWFpbCIsImVtYWlsX3ZlcmlmaWVkIjpmYWxzZSwicHJlZmVycmVkX3VzZXJuYW1lIjoiYWxlbi50dW5pbmcifQ.jNL_JRk7bDfcQ52A6a8ScK0iGaVFU4DtAo25ecBmeH9Xqu14NtUSfXoDhwWWsL3qzs_nWvMPQsc_AJHA03788y3kJBG4XRxCIC_q2y7iRwOFQTHB4cYaOQr8617xAhJrOGCHJYZHMtaYQo-WItvvPLTJoFLkfaIRl2H1nQNJ__04MmLJ7s_7uQ7HUPpDly2QMipaWj3nlapBaHrNSrusPIKI31FMpcq3ej2GZeJhC2r5rcDhDLBdl-_eYZEkgkHyF2cQ7TmtH69NJMPZ9bOGKwh6dcxh_7YNev5WeGy723lMaaiz4qjOyD2KHe1esoX-4YP2ZHh0JbTRgb3sfcHDvQ"
}


### Deploy the changes to Kubernetes in Dev Mode

Step 1: Go to Developer Dashboard tab. It will provide you with the IDE along with the integrated terminal. 

Step 2: Click on the bottom status bar and select `TERMINAL`.

k8s folder contains all the manifest files and defines the deployment strategy for the application. 

Step 3: Execute the command below. 

```execute
kubectl apply -f k8s/
```

In this example , we use `Skaffold` which simplifies local development. You can deploy the application is DEV mode which keeps watching for the files changes and on any change, triggers the entire deployment process automatically without the user having to run and manage it manually.

```execute
skaffold dev
```

On exiting the command, Skaffold will automatically destroy all the resources it created with the above command.


Note: You can also use the `skaffold run` to deploy the changes onto Kubernetes in normal mode. In this mode, the resources created by the user remain unless he deletes them.

### Clean up the Application Resources

You can delete all the application resources created by executing the following command:

```execute
skaffold delete
```

### Conclusion

Now Keycloak authentication is added to your sample application.
