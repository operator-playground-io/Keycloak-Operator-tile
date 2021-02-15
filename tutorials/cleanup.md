---
title: Keycloak Operator cleanup Tutorial
description: This tutorial explains how to cleanup Operator
---


### Cleaning Up Operator



***Delete the operator's custom resource by kubectl delete commands :***

Example:
 
 ```execute
 kubectl delete -f KeycloakInstance.yaml
 ```



***Delete the operator by kubectl delete command:***
 
 
 Example:
 
 ```execute
 kubectl delete -f https://operatorhub.io/install/keycloak-operator.yaml
 ```
 

 
***Delete all the yaml files:***
 
 Example:
 
  ```execute
  rm -rf KeycloakInstance.yaml
  ```
  
