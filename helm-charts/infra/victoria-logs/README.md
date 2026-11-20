# Install/Upgrade
```
helm dependency update
helm upgrade --install --atomic --timeout 5m --namespace victoria-logs --create-namespace -f values.yaml victoria-logs .
```

# Uninstall
```
helm uninstall --namespace victoria-logs victoria-logs
```

# Render templates
```
helm dependency update
helm template --namespace victoria-logs -f values.yaml .
```
