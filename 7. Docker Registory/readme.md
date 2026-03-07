# Docker Registry Guide

## 1️⃣ Create a Repository on Docker Hub

1. Go to: [https://hub.docker.com](https://hub.docker.com)
2. Click **Create Repository**.
3. Give it a name (example: `flask-mysql-app`).
4. Set visibility:
   - **Public** (recommended for portfolio projects)
   - **Private** (if needed)

**Example repo name:** `raviagrahari/flask-mysql-app`

**Structure:** `<dockerhub-username>/<repo-name>`

## 2️⃣ Login to Docker Hub from EC2

SSH into your EC2 instance and run:

```bash
docker login
```

Enter:
- **Username:** `your-dockerhub-username`
- **Password:** `your-dockerhub-password`

If successful, you will see:
```text
Login Succeeded
```

## 3️⃣ Check Your Docker Image

List images:

```bash
docker images
```

**Example output:**
```text
REPOSITORY        TAG       IMAGE ID
flask-app         latest    a1b2c3d4
mysql-db          latest    e5f6g7h8
```

## 4️⃣ Tag the Image for Docker Hub

Docker Hub requires the image to follow this format: `dockerhub-username/repository-name:tag`

**Example:**
```bash
docker tag flask-app raviagrahari/flask-mysql-app:latest
```

**Verify:**
```bash
docker images
```

Now you should see:
```text
raviagrahari/flask-mysql-app   latest
```

## 5️⃣ Push Image to Docker Hub

Run:

```bash
docker push raviagrahari/flask-mysql-app:latest
```

**Example output:**
```text
The push refers to repository [docker.io/raviagrahari/flask-mysql-app]
layer1: pushed
layer2: pushed
latest: digest: sha256:xxxxx
```

## 6️⃣ Verify on Docker Hub

Open your repository: [https://hub.docker.com/r/raviagrahari/flask-mysql-app](https://hub.docker.com/r/raviagrahari/flask-mysql-app)

You will see the uploaded image.

## 7️⃣ Pull the Image Anywhere (Verification)

Test by pulling it:

```bash
docker pull raviagrahari/flask-mysql-app:latest
```