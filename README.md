# 🚀 Spring Boot CI/CD Pipeline using Jenkins, Docker & Docker Compose

This project demonstrates a complete CI/CD pipeline for a Spring Boot application using Jenkins, Docker, Docker Hub, and Docker Compose. The pipeline automatically builds, containerizes, pushes, and deploys the application whenever code is pushed to GitHub.

---

## 🧰 Tech Stack

* Backend: Spring Boot (Java 21)
* Build Tool: Maven
* CI/CD: Jenkins (Declarative Pipeline)
* Containerization: Docker
* Container Orchestration: Docker Compose
* Image Registry: Docker Hub
* Version Control: GitHub

---

## 📂 Project Structure

```
.
├── src/                    # Spring Boot source code
├── target/                 # Maven build output (JAR)
├── Dockerfile              # Docker image definition
├── docker-compose.yml      # Container deployment configuration
├── Jenkinsfile             # CI/CD pipeline definition
├── pom.xml                 # Maven configuration
└── README.md               # Project documentation
```

---

## 🔄 CI/CD Workflow

1. Developer pushes code to GitHub
2. GitHub Webhook triggers Jenkins pipeline
3. Jenkins stages:

   * Checkout source code
   * Build Spring Boot JAR using Maven
   * Build Docker image
   * Login to Docker Hub using access token
   * Push image to Docker Hub
   * Deploy application using Docker Compose
4. Application runs automatically in a Docker container

---

## 🐳 Dockerfile

The Dockerfile is optimized for CI/CD and does **not** contain any credentials.

```dockerfile
FROM eclipse-temurin:21-jdk-alpine
WORKDIR /app
COPY target/*.jar app.jar
EXPOSE 9090
ENTRYPOINT ["java", "-jar", "app.jar"]
```

---

## 📦 Docker Compose

Docker Compose is used to pull the latest image from Docker Hub and run the container.

```yaml
version: "3.8"

services:
  springboot-app:
    image: dockerhub-username/springboot-ci-cd:latest
    container_name: springboot-ci-cd
    ports:
      - "9090:9090"
    restart: always
```

---

## 🔐 Credentials Management

* Docker Hub credentials are stored securely in Jenkins Credentials Manager
* Authentication is done using a Docker Hub Access Token
* No secrets are stored in the repository

---

## ▶️ How to Run Locally (Optional)

```bash
mvn clean package

docker build -t springboot-ci-cd .

docker compose up -d
```

Access the application:

```
http://localhost:9090
```

---

## 🧠 Key Highlights

* Fully automated CI/CD pipeline
* Secure credential handling
* Docker best practices followed
* Production-style deployment using Docker Compose
* Interview-ready DevOps project

---

## 📌 Future Enhancements

* Push images with version tags
* Blue-Green deployment
* Deploy on AWS EC2
* Add monitoring (Prometheus + Grafana)

---

## 👤 Author

Jaba Raj V
DevOps & Cloud Enthusiast

---

⭐ If you like this project, don’t forget to star the repository!


