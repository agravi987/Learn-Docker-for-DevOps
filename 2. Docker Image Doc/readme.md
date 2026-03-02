# 🐳 Docker Image Documentation

> A beginner‑friendly guide with commands explained and brought to life by emojis!

---

## 1. 🛠️ Ubuntu-Based Setup Guide

This section walks you through installing Docker on an Ubuntu system. Each command is shown with its purpose.

### Step 1: Update System Packages 🔄
This fetches the latest package lists and upgrades installed packages.
```bash
sudo apt update      # refresh package list
sudo apt upgrade -y  # install newest versions
```

### Step 2: Install Docker Engine 🐋
Installs Docker's core software (`docker.io` package).
```bash
sudo apt install docker.io -y
```

### Step 3: Verify Installation ✅
Check that Docker is installed and view its version.
```bash
docker --version    # prints Docker version information
```

You should see something like:
```
Docker version XX.X.X, build XXXXX
```

### Step 4: Enable and Start the Docker Service ▶️
Enable Docker so it starts at boot, then start and check its status.
```bash
sudo systemctl enable docker   # enable service at startup
sudo systemctl start docker    # start service now
sudo systemctl status docker   # display current state
```

Expected output will include `Active: active (running)`.

---

## 2. 👤 Run Docker as Non-Root

Docker commands require root by default. Add yourself to the `docker` group to run them without `sudo`.

### Add Your User to the Docker Group 🧑‍🤝‍🧑
```bash
sudo usermod -aG docker $USER    # append current user to group
```
If your username is `ubuntu`:
```bash
sudo usermod -aG docker ubuntu
```

### Apply Group Changes 🔁
```bash
newgrp docker   # re-evaluates your group membership immediately
```
Or simply log out and log back in.

### Test Without sudo 🧪
```bash
docker run hello-world  # runs a simple container to confirm access
```
If it prints a welcome message, you're good to go! ✅

---

## 3. 📦 What Is a Docker Image?
A Docker image is a read-only template containing everything needed to run an application (code, runtime, libraries, etc.).
Images are pulled from registries such as **Docker Hub**.

---

## 4. 📥 Pulling Images
Retrieve images from a registry; they are stored locally after download.

```bash
docker pull ubuntu          # latest Ubuntu image
```
```bash
docker pull ubuntu:22.04    # specific tag/version
```

The first time you pull an image it downloads all layers; subsequent pulls are faster thanks to caching.

---

## 5. 📚 Listing Local Images
Show which images you've downloaded.

```bash
docker images     # list all images in local cache
```

| Column      | Meaning                         |
|-------------|---------------------------------|
| REPOSITORY  | Name of the image               |
| TAG         | Version or tag string           |
| IMAGE ID    | Unique hash identifier          |
| CREATED     | When it was built               |
| SIZE        | Disk size                       |

---

## 6. 🔍 Inspecting an Image
Get detailed metadata (configuration, layers, environment variables, etc.).

```bash
docker inspect ubuntu
```

---

## 7. ▶️ Running Containers
Images become containers when executed.

### Interactive (foreground) mode 💬
```bash
docker run -it ubuntu bash
```
`-it` attaches your terminal to the container so you can interact with a shell.

### Detached (background) mode 🛌
```bash
docker run -d nginx
```
`-d` runs the container in the background; useful for services.

---

## 8. 📊 Listing Containers

```bash
docker ps       # show running containers
```
```bash
docker ps -a    # show all containers, including stopped ones
```

---

## 9. 🛑 Stopping & Removing Containers

```bash
docker stop <container_id>   # stop a running container
```
```bash
docker rm <container_id>     # remove a stopped container
```

Replace `<container_id>` with the ID from `docker ps`.

---

## 10. 🗑️ Removing Images

```bash
docker rmi ubuntu        # delete the specified image
```
```bash
docker rmi -f ubuntu     # force removal even if child images exist
```

Use force cautiously; it can break dependent images.

---

## 11. 🔎 Searching the Registry
Look for public images by keyword.

```bash
docker search nginx
```

---

## 12. 🏷️ Tagging Images
 Tags let you label images before pushing them to a registry.

```bash
docker tag ubuntu:22.04 myubuntu:v1  # create a new tag
```

Tags follow the format `name:tag`.

---

## 13. 📤 Pushing Images to Docker Hub
Share your custom images!

1. **Login** to your Docker Hub account:
```bash
docker login
```
2. **Tag** the image with your username:
```bash
docker tag myimage username/myimage:v1
```
3. **Push** the tagged image:
```bash
docker push username/myimage:v1
```

Now anyone can pull your image from Docker Hub.

---

## 💡 Important Notes

- **Images are layered**; reused layers speed up builds.
- **Containers are ephemeral**; data disappears unless you use volumes.
- **Avoid `latest` in production** – use explicit version tags.
- **Prune unused resources** to free disk space:
```bash
docker image prune   # remove dangling images
```

Happy Dockering! 🚢
