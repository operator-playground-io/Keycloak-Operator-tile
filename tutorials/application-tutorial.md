---
title: Keycloak Operator Sample Application Tutorial
description: This tutorial explains how to use an Keycloak cluster created by the operator in an application.
---

### Introduction

Sample application is a Node.js application which is deployed as a microservice.
The example also uses Skaffold which handles the workflow for building, pushing and deploying your application, allowing you to focus on what matters most: writing code.

### Code Structure

![codestructure](_images/keycloak-sample-app-structure..png)

It follows a simple modular and MVC pattern. There are 2 folders that are of our interest:
- k8s :  This contains all the deployment and service yaml for the application. This defines the deployment and exposure of our application.
- k8s_keycloak :  This contains all the deployment and service yaml for creating an Keycloak cluster if you need for example to run the application locally.


### Try the example

**Step 1:** 

Perform the following steps described in the tutorials.

- Install the Keycloak operator.
- Create an Keycloak cluster.
- Login to Keycloak Admin Console.
- Create a realm with name 'myrealm'.
- Create an user. You will need the user name and password to log in into the application.
- Create a client with name 'vanilla'.

**Step 2:** Install the application sample

Get sample code:
```execute
cd /home/student/projects && git clone https://github.com/Andi-Cirjaliu/edge-keycloak-sample.git
```

Navigate to the example:
```execute
cd edge-keycloak-sample
```

Set the Keycloak instance IP:
```execute
export ip_addr=$(ifconfig eth1 | grep inet | awk '{print $2}' | cut -f2 -d:)
```
```execute
sed -i "s/ip-address/$ip_addr/" .env
```

Setup skaffold default repository to the local one:
```execute
skaffold config set default-repo localhost:5000
```

Install and start the sample. To stop and remove the application you will need to follow the steps from **Clean up the Kubernetes resources**.
```execute
skaffold run
```
Alternatively you can use this command to install the sample, watch for code changes and re-deploy the application automatically.
On exiting the command, Skaffold will automatically stop and delete the sample application. 
```execute
skaffold dev
```

### Access the application

Click on the Key icon on the dashboard and copy the value under the `DNS` section and `IP` field

URL :  http://##DNS.ip##:30300

### Deploy changes to Kubernetes in Dev Mode

Go to Developer Dashboard tab, it will provide you with the IDE along with the integrated terminal.  Click on the bottom status bar and select `TERMINAL`. 

k8s folder contains all the manifest files and defines the deployment strategy for the application.
One can execute them using :

```execute
kubectl apply -f k8s/
```

In this example , we use `Skaffold` which simplifies local development. You can deploy the application is DEV mode which keeps watching for the files changes and on any change, triggers the entire deployment process automatically without the user having to run and manage it manually.

```execute
skaffold dev
```

On exiting the command, Skaffold will automatically destroy all the resources it created with above command.


Also, you can use the `skaffold run` to deploy the changes onto Kubernetes as a normal mode. In this mode, the resources created remains unless the user deletes them.

### Clean up the Kubernetes resources

You can delete all the application resources created by executing the following command:

```execute
skaffold delete
```
