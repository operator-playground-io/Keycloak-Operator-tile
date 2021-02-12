<h1 align="center">Keycloak Operator</h1> 

![Logo](_images/keycloak-logo.png)



### Overview:

A Kubernetes Operator based on the Operator SDK for installing and managing Keycloak.The Keycloak Operator automates Keycloak administration in Kubernetes or Openshift. You use this Operator to create custom resources (CRs), which automate administrative tasks. 
Keycloak lets you add authentication to applications and secure services with minimum fuss. No need to deal with storing users or authenticating users. It's all available out of the box.

The operator can deploy and manage Keycloak instances on Kubernetes and OpenShift. 

### Operator's features are as follows:

Install Keycloak to a namespace
Import Keycloak Realms
Import Keycloak Clients
Import Keycloak Users
Create scheduled backups of the database
Install Extensions


### Objective of tutorial

In this tutorial,we are going to cover following topics:

1. How to Install Keycloak Operator and verify its successful installation.
2. Create Keycloak Cluster Instance using Keycloak Operator.
3. Login to Keycloak Admin Console with Keycloak Operator.
4. Create Keycloak Realm. 
5. Create Keycloak User.
6. Create a Client and authenticate a sample application using Keycloak server.
7. Cleanup Operators.
  
