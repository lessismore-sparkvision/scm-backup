# Build and push image to Azure using `docker-compose`

To push your images to Azure Container Registry (ACR), follow these steps:

**Prerequisites:**

- An Azure Container Registry (ACR) is created.
- You are authenticated to Azure (using az login).
- Docker CLI is authenticated to your ACR:

```bash
az acr login --name <ACR_NAME>
```

**Steps:**

1. Update your docker-compose.yml file to tag images for ACR:

```yaml
services:
  scmbackup:
    build:
      context: .
      dockerfile: src/ScmBackup/Dockerfile
    image: <ACR_NAME>.azurecr.io/scmbackup:1.0
```

2. Build and tag the images:

```bash
docker-compose build
```

3. Push the images to ACR:

```bash
docker-compose push
```

# Secrets

Make sure that secrets are not stored in your images or `.env` file, but are defined as environmental variables, as docker secrets
or in a KeyVault.

For debugging purposes a template `.env` file is defined below.

```env
APP_ID=1000
BACKUP_DIR=C:/scm-backup
ACR_NAME=my-acr.azurecr.io
BITBUCKET_PASSWORD=my-secret-bitbucket-password
GITHUB_PASSWORD=my-secret-github-password
GITLAB_PASSWORD=my-secret-gitlab-password
```
