# Install/Upgrade
```
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.21.3/cert-manager.crds.yaml
helm dependency update
helm upgrade --install --atomic --timeout 5m --namespace cert-manager --create-namespace cert-manager .
```

# Uninstall
```
helm uninstall --namespace cert-manager cert-manager
```

# Render templates
```
helm dependency update
helm template --namespace cert-manager cert-manager .
```
