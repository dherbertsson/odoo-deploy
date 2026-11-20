# Install/Upgrade
```
helm dependency update
helm upgrade --install --atomic --timeout 5m --namespace odoo-instance-1 --create-namespace -f values.yaml -f ../shared-values.yaml odoo-instance-1 .
```

# Uninstall
```
helm uninstall --namespace odoo-instance-1 odoo-instance-1
```

# Render templates
```
helm dependency update
helm template --namespace odoo-instance-1 -f values.yaml -f ../shared-values.yaml .
```
