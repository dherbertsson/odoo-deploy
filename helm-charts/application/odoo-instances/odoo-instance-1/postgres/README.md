# Install/Upgrade
```
helm dependency update
helm upgrade --install --wait --namespace odoo-instance-1 --create-namespace -f values.yaml -f ../shared-values.yaml odoo-instance-1-postgres .
```

# Uninstall
```
helm uninstall --namespace odoo-instance-1 odoo-instance-1-postgres
```

# Render templates
```
helm dependency update
helm template -f values.yaml -f ../shared-values.yaml .
```
