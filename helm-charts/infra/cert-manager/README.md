# Install/Upgrade
```
helm dependency update
helm upgrade --install --wait --namespace cert-manager --create-namespace -f values.yaml cert-manager .
```

# Uninstall
```
helm uninstall --namespace cert-manager cert-manager
```

# Render templates
```
helm dependency update
helm template .
```
