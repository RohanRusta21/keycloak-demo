# keycloak-demo


# Helm chart for keycloak

```bash
helm repo add codecentric https://codecentric.github.io/helm-charts
```

```bash
helm repo list
```

```bash
helm install keycloak codecentric/keycloak --values codecentric.yaml
```

```bash
helm show values codecentric/keycloak > mykeycloak.yml (you can give any name)
```

# Add the below in above yml file under postgresql section 

```bash
persistence:
  existingClaim: Keycloak-volume
```

# Update the helm repo chart

```bash
helm repo update
```

```bash
helm install keycloak1 codecentric/keycloak (keycloak1=New Release)
```
