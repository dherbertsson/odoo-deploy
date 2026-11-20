# Install/Upgrade
```
helm upgrade --install --atomic --timeout 5m --namespace infisical infisical-service-accounts .
```

# Uninstall
```
helm uninstall --namespace infisical infisical-service-accounts
```

# Render templates
```
helm template .
```
