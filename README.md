# keycloak-demo


# Helm chart for keycloak

```bash
helm repo add codecentric https://codecentric.github.io/helm-charts
```

```bash
helm repo list
```

```bash
helm install keycloak codecentric/keycloak
```

```bash
helm show values codecentric/keycloak > mykeycloak.yml (you can give any name)
```

# Add the below in above yml file under postgresql section 

```bash
persistence:
  existingClaim: keycloak-volume
```

# Update the helm repo chart

```bash
helm repo update
```

```bash
helm install keycloak codecentric/keycloak --values mykeycloak.yml (keycloak=Release Name)
```

```bash
kubectl edit svc keycloak-http
```

# Add initial credentials for keycloak (Inside extraenv section)

```bash
- name: KEYCLOAK_USER
  value: admin
- name: KEYCLOAK_PASSWORD
  value: admin
```

# To Access the admin console , we have to edit the sts of keycloak and add the url to solve headers/CORS issue

```bash
kubectl get sts
```

```bash
kubectl edit sts keycloak
```

Below keycloak username & password, write this 

```bash
- name: KEYCLOAK_FRONTEND_URL
  value: "https://47416113-7b47-49d5-9257-921ae293c284-10-244-6-40-31218.papa.r.killercoda.com/auth/" # Killercoda server url 
```

After Login & Creatin the user/realm from UI, Validate that it is stored in our Postgres PV or not

```bash
kubectl get pv
```

```bash
kubectl describe pv keycloak-pv
```

# To check that user is saved in database or not

```bash
ssh node01
```

```bash
kubectl exec -it keycloak-postgresql-0 -- bash
```

```bash
psql -U keycloak -d keycloak
```

# For fetching postgres password

```bash
kubectl get secret
kubectl get secret keycloak-postgresql -o jsonpath="{.data.postgresql-password}" | base64 --decode
```

# Query to check that user is there or not

```bash
SELECT * FROM user_entity WHERE username = 'admin';
```
