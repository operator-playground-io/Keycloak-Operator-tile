<h1 align="center">Keycloak Operator</h1> 

![Logo](_images/keycloak-logo.png)



### Overview:

Keycloak operator is a Kubernetes Operator based on the Operator SDK for installing and managing Keycloak. This operator automates the Keycloak administration  in Kubernetes  or Openshift. 
Keycloak operator is typically used for creating custom resources (CRs), which automate administrative tasks. It allows application authentication and secure service authentication with minimum fuss. It also reduces the overheads of user management that includes storing users or authenticating users.

The operator can deploy and manage Keycloak instances on Kubernetes and OpenShift. 

### Features of Keycloak Operator

- Install Keycloak to a namespace

- Import Keycloak Realms

- Import Keycloak Clients

- Import Keycloak Users

- Create Scheduled Backups of the database

- Install Extensions


### Objective of the tutorial

In this tutorial,we are going to cover following topics:

1. Install Keycloak Operator and Verify its Successful Installation.
2. Create Keycloak Cluster Instance using Keycloak Operator.
3. Access Keycloak Admin Console using Keycloak Operator.
4. Create a Keycloak Realm. 
5. Create a Keycloak User.
6. Create a Client and Authenticate a Sample Application using Keycloak server.
7. Cleanup the Keycloak Operator.
  
