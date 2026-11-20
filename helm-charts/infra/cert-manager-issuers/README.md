# Install/Upgrade
```
helm upgrade --install --atomic --timeout 5m --namespace cert-manager -f values.yaml cert-manager-issuers .
```

# Uninstall
```
helm uninstall --namespace cert-manager cert-manager-issuers
```

# Render templates
```
helm template --namespace cert-manager -f values.yaml cert-manager-issuers .
```
