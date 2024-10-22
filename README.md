# Vault on OpenShift

## Installation

```
helm repo add hashicorp https://helm.releases.hashicorp.com

helm install vault hashicorp/vault --set "global.openshift=true"
```

## Configuration

Initialization: 

```
oc exec -ti vault-0 -- vault operator init
```

Unseal Vault (3x)

```
oc exec -ti vault-0 -- vault operator unseal
oc exec -ti vault-0 -- vault operator unseal
oc exec -ti vault-0 -- vault operator unseal
```

Login 

```
oc exec -ti vault-0 -- vault login
```

Enable secrets engine

```
oc exec -ti vault-0 -- vault secrets enable -path=campnow kv
```

Create secret

```
oc exec -ti vault-0 -- vault kv put -mount=campnow/ hello foo=world
```

### Links

[Installation of Vault on OpenShift with helm](https://developer.hashicorp.com/vault/docs/platform/k8s/helm/openshift)

# External Secrets on OpenShift

Installation

```
helm repo add external-secrets https://charts.external-secrets.io

helm install external-secrets \
   external-secrets/external-secrets \
    -n external-secrets \
    --create-namespace
```


```
oc apply -f vault-secret-store.yaml
oc apply -f test-external-secret.yaml
```

### Links

[Install External Secrets on OpenShift](https://github.com/external-secrets/external-secrets)
[Connect External Secrets to Vault](https://external-secrets.io/latest/provider/hashicorp-vault/)