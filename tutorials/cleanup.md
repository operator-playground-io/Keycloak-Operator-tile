---
title: Keycloak Operator cleanup 
description: Learn how to clean up Keycloak Operator and its resources.
---


### Cleaning Up Operator


**Step 1: Delete the operator's Custom Resources by using `kubectl delete` commands as below.**

 
 ```execute
 kubectl delete -f KeycloakInstance.yaml
 ```



**Step 2: Delete the operator by using `kubectl delete` command as below.**
 
 
 
 ```execute
 kubectl delete -f https://operatorhub.io/install/keycloak-operator.yaml
 ```
 

 
**Step 3: Delete all the yaml files.**
 

 
  ```execute
  rm -rf KeycloakInstance.yaml
  ```
  
