# Install/Upgrade
```
helm dependency update
helm upgrade --install --wait --namespace victoria-logs --create-namespace -f values.yaml victoria-logs .
```

# Uninstall
```
helm uninstall --namespace victoria-logs victoria-logs
```

# Render templates
```
helm dependency update
helm template -f values.yaml .
```
