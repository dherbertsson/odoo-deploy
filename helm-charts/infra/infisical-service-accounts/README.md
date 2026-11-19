# Install/Upgrade
```
helm dependency update
helm upgrade --install --wait --namespace infisical infisical-service-accounts .
```

# Uninstall
```
helm uninstall --namespace infisical infisical-service-accounts
```

# Render templates
```
helm dependency update
helm template .
```
