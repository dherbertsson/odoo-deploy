# Install/Upgrade
```
helm dependency update
helm upgrade --install --atomic --timeout 5m --namespace infisical --create-namespace -f values.yaml --set authSecret=$(openssl rand -base64 32) --set encryptionKey=$(openssl rand -hex 16) infisical .
```

# Uninstall
```
helm uninstall --namespace infisical infisical
```

# Render templates
```
helm dependency update
helm template -f values.yaml --set authSecret=$(openssl rand -base64 32) --set encryptionKey=$(openssl rand -hex 16) .
```
