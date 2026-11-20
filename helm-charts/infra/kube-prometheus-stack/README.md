# Install/Upgrade
```
helm dependency update
helm upgrade --install --wait --namespace prometheus --create-namespace kube-prometheus-stack .
```

# Uninstall
```
helm uninstall --namespace prometheus kube-prometheus-stack
```

# Render templates
```
helm dependency update
helm template .
```
