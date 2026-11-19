# Install/Upgrade
```
helm dependency update
helm upgrade --install --wait --namespace infisical --set identityId=ID infisical-connection .
```
Note that `ID` needs to be replaced with the Machine Identity created in https://infisical.com/docs/documentation/guides/kubernetes-operator#create-a-machine-identity.

# Uninstall
```
helm uninstall --namespace infisical infisical-connection
```

# Render templates
```
helm dependency update
helm template --set identityId=ID .
```
