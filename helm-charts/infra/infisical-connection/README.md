# Install/Upgrade
```
helm upgrade --install --atomic --timeout 5m --namespace infisical --set identityId=ID infisical-connection .
```
Note that `ID` needs to be replaced with the Machine Identity created in https://infisical.com/docs/documentation/guides/kubernetes-operator#create-a-machine-identity.

# Uninstall
```
helm uninstall --namespace infisical infisical-connection
```

# Render templates
```
helm template --set identityId=ID .
```
