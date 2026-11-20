# Install/Upgrade
```
helm dependency update
helm upgrade --install --atomic --timeout 5m --namespace cloudnative-pg --create-namespace -f values.yaml cloudnative-pg .
```

# Uninstall
```
helm uninstall --namespace cloudnative-pg cloudnative-pg
```

# Render templates
```
helm dependency update
helm template --namespace cloudnative-pg -f values.yaml .
```
