# TeSS Openshift helm chart

## USE

First, you need to run `helm dependency build` to download the [Redis Helm Chart](https://github.com/bitnami/charts/tree/main/bitnami/redis)

Two secrets must be created beforehand. It will contain:

- The `redis-password-secret` secret to allow the Redis pods to communicate with each other.

- The `redis-acl` secret to TeSS to connect to the Redis Master pod.

To create these two secrets, you can run this command: (you must be connected to your Rahti project and [oc](https://docs.csc.fi/cloud/rahti/usage/cli/) command line must be installed)

```
oc create secret generic redis-acl --from-literal="allas-ui=$(python3 -c 'import secrets; print(secrets.token_hex(16))')" &&
oc create secret generic redis-password-secret --from-literal="redis-password=$(python3 -c 'import secrets; print(secrets.token_hex(16))')"
```

Once done, you can run `helm install production .`

