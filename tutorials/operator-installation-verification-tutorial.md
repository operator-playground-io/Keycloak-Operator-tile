---
title: Keycloak Operator Installation Verification.
description: Learn how to verify that the Keycloak Operator has been installed properly in the namespace.
---

### Check the Keycloak Operator

**Step 1: Verify that the Keycloak Operator has been installed successfully by executing below command.**

```execute
kubectl get csv -n my-keycloak-operator
```

You will see a similar output as below.

```output
NAME                        DISPLAY             VERSION   REPLACES                    PHASE
keycloak-operator.v12.0.1   Keycloak Operator   12.0.1    keycloak-operator.v11.0.0   Succeeded
```

It may take a few minutes. Please wait for the PHASE STATUS to be SUCCEEDED, then continue.

**Step 2: Check the pod status.**

Check the Operator’s pod by running the following command.

```execute
kubectl get pods -n my-keycloak-operator
```

From above, you can see the pod with:
a.	NAME starting with 'Keycloak-operator'
b.	READY value is '1/1'
c.	STATUS is `Running`


```output
NAME                                 READY   STATUS    RESTARTS   AGE
keycloak-operator-668cc5dc75-krw9m   1/1     Running   0          92s
```


### Conclusion

The steps described above assist you in verifying the successful installation of Keycloak Operator.
