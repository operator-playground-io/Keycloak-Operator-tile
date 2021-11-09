---
title: Secure an React Application using Keycloak.
description: Learn how to use a Keycloak cluster to add authentication to an applications and secure the services.
---


### Introduction

The sample application we have considered here is a React application. The application runs in a Node.js server. The example also uses Skaffold tool which handles the workflow for building, pushing and deploying an application, allowing the developer to focus on writing the code.

### Code Structure

![codestructure](_images/keycloak-react-app-structure.png)

The code stucture follows a simple modular and MVC pattern. There are 3 folders that are of our interest:

	- k8s : This folder contains all the deployment and service yaml files for the application. This defines the deployment and exposure of our application.
	- k8s_keycloak : This folder contains all the deployment and service yaml files for creating an a Keycloak cluster if you need, for example to run the application locally.
	- src : the sources for React application are in this folder


### Try the example

**Step 1: Perform the following steps described in the tutorials.**

*  Install the Keycloak operator.

*  Create an Keycloak cluster.

*  Login to Keycloak Admin Console.

*  Create a realm with name 'myrealm'.

*  Create a client with name 'vanilla'. Use the following URL: http://##DNS.ip##:30400

*  Optional: Create 'app-user' role if does not exist. Click on Roles, click on Add role button. Enter 'app-user' as the name of the new role.

*  Create an user. You will need the user name and password to log in into the application. If you have created 'app-user' role, assign it to the new user. To do this click on 'Role mappings', select 'app-user' role from the list of available roles and click on 'Add selected'.


Once you complete the above steps, proceed with following steps to execute the sample application.


**Step 2: Install the sample application.**

- Get the sample code.

```execute
cd /home/student/projects && git clone https://github.com/operator-playground-io/keycloak-react-sample.git
```

- Navigate to the example.

```execute
cd keycloak-react-sample
```

- Set the Keycloak instance IP.

```execute
export ip_addr=$(ifconfig eth1 | grep inet | awk '{print $2}' | cut -f2 -d:)
```
```execute
sed -i "s/ip-address/$ip_addr/" .env
```

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

http://##DNS.ip##:30400


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

Now Keycloak authentication is added to your React sample application.
