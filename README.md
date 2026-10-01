# Java Web Application with Automated CI/CD

## Features
- Spring Boot REST endpoints: `/` and `/health`
- Maven build, JUnit tests, and JAR packaging
- Docker image build and push to Docker Hub
- GitHub Actions automatically runs on pushes and pull requests to `main`
- Docker publishing only runs on successful pushes to `main`

## Prerequisites
- JDK 21 and Maven (for local builds)
- Docker (for local container runs)
- GitHub repository and Docker Hub account

## Run locally
```bash
mvn clean verify
mvn spring-boot:run
```
Open `http://localhost:8080/` or `http://localhost:8080/health`.

## Run with Docker locally
```bash
mvn clean package
docker build -t java-cicd-demo:local .
docker run --rm -p 8080:8080 java-cicd-demo:local
```

## Configure automated Docker publishing
1. Create a Docker Hub repository named `java-cicd-demo`.
2. In GitHub, open **Settings → Secrets and variables → Actions**.
3. Add repository secrets:
   - `DOCKERHUB_USERNAME`: your Docker Hub username
   - `DOCKERHUB_TOKEN`: a Docker Hub access token (do not use your account password)
4. Push this project to the `main` branch.

## CI/CD behavior
- Push or pull request to `main`: checks out code, installs Java 21, runs `mvn clean verify`, and stores the JAR artifact.
- Successful push to `main`: rebuilds the JAR, builds the Docker image, and pushes `latest` and the commit SHA tag to Docker Hub.
- Pull requests do not publish Docker images.

## Pull and run the published image
```bash
docker pull YOUR_DOCKERHUB_USERNAME/java-cicd-demo:latest
docker run --rm -p 8080:8080 YOUR_DOCKERHUB_USERNAME/java-cicd-demo:latest
```
Then visit `http://localhost:8080/`.

## Notes
This pipeline publishes the image to Docker Hub. It does not deploy to a cloud server or production environment; add a deployment job and target credentials if deployment is required.
