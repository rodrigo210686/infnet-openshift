### Criação do projeto

```bash
# Criar o projeto multiplayer-app
oc new-project multiplayer-app \
  --display-name="Multi-Layer Application" \
  --description="WordPress com MySQL - Aplicação Multi-Camadas"

```
---

## Criação dos Secrets

### Secret para MySQL

```bash
# Criar secret com credenciais do MySQL
oc create secret generic mysql-secret \
  --from-literal=MYSQL_ROOT_PASSWORD='password' \
  --from-literal=MYSQL_DATABASE='wordpress' \
  --from-literal=MYSQL_USER='wpuser' \
  --from-literal=MYSQL_PASSWORD='password' \
  -n multiplayer-app

### Criar Secret para WordPress

```bash
# Criar secret com credenciais do WordPress
oc create secret generic wordpress-secret \
  --from-literal=WORDPRESS_DB_PASSWORD='password' \
  -n multiplayer-app

```

---

## Criação de ConfigMaps

```bash
# Criar ConfigMap com configurações do MySQL
oc create configmap mysql-config \
  --from-literal=MYSQL_DATABASE='wordpress' \
  --from-literal=MYSQL_USER='wpuser' \
  -n multiplayer-app
```

### Criar ConfigMap para WordPress

```bash
# Criar ConfigMap com configurações do WordPress
oc create configmap wordpress-config \
  --from-literal=WORDPRESS_DB_HOST='mysql' \
  --from-literal=WORDPRESS_DB_USER='wpuser' \
  --from-literal=WORDPRESS_DB_NAME='wordpress' \
  -n multiplayer-app
```
# Deploy statefulset

[Statefulset](./01-mysql-statefulset.yaml)
