🐳 Dockerizing a Simple Java Application

(Step-by-Step Documentation with Command Explanation)

📌 Objective

To:

Clone a Java project

Create a custom Dockerfile

Build a Docker image

Run the containerized Java application

1️⃣ Verify Required Tools

Before starting, ensure Docker and Git are installed.

Check Docker Installation
docker images
docker ps

Purpose:

You created a structured folder layout:



🔁 Your Iterations

# 🐳 Dockerizing a Simple Java Application

> Step-by-step guide with command explanations and friendly emojis.

---

## 🎯 Objective

- Clone a Java project
- Create a Dockerfile for the app
- Build a Docker image
- Run the containerized Java application

---

## ✅ Prerequisites

Make sure you have Docker and Git installed on your machine.

Check Docker:
```bash
docker --version       # shows Docker version
docker images          # lists local images
docker ps              # lists running containers
```

Check Git:
```bash
git --version          # confirms Git is installed
```

---

## 1. Clone the Repository

```bash
git clone https://github.com/LondheShubham153/simple-java-docker.git
```

Purpose: copies the project to your local machine (folder `simple-java-docker/`).

---

## 2. Organize the Project (optional)

```bash
mkdir projects
mv simple-java-docker/ projects/
cd projects/simple-java-docker/
ls
```

Why: keeps your workspace tidy — `ls` shows `src/`, `Dockerfile` (if present), and Java files.

---

## 3. Review or Create the `Dockerfile`

If a `Dockerfile` exists, inspect it:
```bash
cat Dockerfile
```

If you want to recreate it, remove and open a new one:
```bash
rm Dockerfile
vim Dockerfile
```

### Final `Dockerfile` used in this guide

```dockerfile
# Use a lightweight JDK base image
FROM eclipse-temurin:17-jdk-alpine

# Set working directory inside container
WORKDIR /app

# Copy Java source into the container
COPY src/Main.java /app/Main.java

# Compile the Java source during build
RUN javac Main.java

# Default command to run the compiled class
CMD ["java", "Main"]
```

---

## 4. Dockerfile Explanation (line-by-line)

- `FROM eclipse-temurin:17-jdk-alpine` — base image with Temurin JDK 17 on Alpine Linux (small, secure).
- `WORKDIR /app` — creates and switches to `/app`; subsequent commands run here.
- `COPY src/Main.java /app/Main.java` — copies the Java source from build context into the image.
- `RUN javac Main.java` — compiles `Main.java` at build time, producing `Main.class` in the image.
- `CMD ["java", "Main"]` — default command when container starts; runs the Java program.

Note: `RUN` executes at image build time; `CMD` runs when a container starts.

---

## 5. Build the Docker Image

```bash
docker build -t java-app .    # builds the image and tags it as 'java-app'
```

What happens:
- Docker reads the `Dockerfile` and executes each instruction, creating image layers.
- The final image is tagged `java-app`.

---

## 6. Verify the Image

```bash
docker images
```

You should see a `java-app` entry under `REPOSITORY`.

---

## 7. Run the Container

```bash
docker run --rm java-app   # runs the container, removes it after exit
```

What this does:
- Docker creates a container from the `java-app` image, executes `CMD` (`java Main`), prints program output, then exits.

Use `--rm` to automatically delete the container after it stops.

---

## 8. Iterative Development

If you change the source or `Dockerfile`, rebuild:
```bash
docker build -t java-app .
```

This updates the image; run it again to test changes.

---

## 9. Image Build Internals (brief)

- Each `Dockerfile` instruction creates a new layer (cached for faster rebuilds).
- Layers: base image → `WORKDIR` layer → `COPY` layer → `RUN javac` layer → final image.

---

## 10. Key Concepts Learned

- Base image selection
- Layered image architecture and caching
- Build context (only files in `.` are accessible during build)
- Difference between `RUN` (build time) and `CMD` (runtime)
- Image tagging and container lifecycle

---

## 11. Improvements & Best Practices

- For multi-file projects, copy the whole project and use a `.dockerignore`:
```dockerfile
COPY . .
```

- Add `.dockerignore` to avoid including unnecessary files in the build context.
- For production, consider building a fat JAR and running with `java -jar app.jar`.

---

Happy Dockering! 🚢 — Ask if you want a multi-stage build, JAR packaging steps, or CI examples.