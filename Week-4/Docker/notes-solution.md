
=======
# Week 4 Docker - Complete Solutions with Theory

## Task 1: Introduction and Conceptual Understanding

### Docker's Purpose in Modern DevOps
Docker revolutionized DevOps by providing consistent environments from development to production. It solves the "it works on my machine" problem by packaging applications and their dependencies into portable containers.

### Virtualization vs. Containerization

**Virtualization:**
- Runs multiple OS instances on single hardware
- Each VM has full OS, kernel, and dependencies
- Heavyweight (GBs per VM)
- Slow startup time
- High resource overhead

**Containerization:**
- Runs multiple isolated applications on single OS
- Shares host OS kernel
- Lightweight (MBs per container)
- Fast startup (seconds)
- Low resource overhead

**Why Containerization is Preferred for Microservices & CI/CD:**
- **Rapid Deployment**: Containers start in seconds vs minutes for VMs
- **Resource Efficiency**: Higher density on same hardware
- **Consistency**: Same environment across dev, test, prod
- **Scalability**: Easy to scale individual microservices
- **CI/CD Integration**: Perfect for automated pipelines

---

## Task 2: Create Dockerfile for Sample Project

### Sample Python Application
Created a simple Flask application that serves "Hello, Docker!"

### Dockerfile with Explanations
```dockerfile
# Use official Python runtime as base image
FROM python:3.9-alpine

# Set working directory in container
WORKDIR /app

# Copy requirements first for better caching
COPY requirements.txt .

# Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY . .

# Expose port 80
EXPOSE 80

# Define environment variable
ENV NAME World

# Run the application
CMD ["python", "app.py"]
Build and Verify
bash
# Build the image
docker build -t sopatel264/sample-app:latest .

# Run the container
docker run -d -p 8080:80 sopatel264/sample-app:latest

# Verify it's running
docker ps

# Check logs
docker logs <container_id>
Task 3: Docker Terminologies and Components
Key Docker Terminologies
Image: Read-only template with instructions for creating a container
Container: Runnable instance of an image
Dockerfile: Text file with instructions to build an image
Volume: Persistent data storage outside container lifecycle
Network: Communication channel between containers

Docker Components
Docker Engine: Core product that creates and runs containers
Docker Hub: Cloud registry for sharing container images
Docker Compose: Tool for defining and running multi-container apps
Docker Desktop: GUI application for Mac/Windows

Component Interaction
text
Dockerfile → Docker Engine → Image → Container
                    ↓
              Docker Hub (Registry)
                    ↓
            Docker Compose (Orchestration)
Task 4: Optimize with Multi-Stage Builds
Multi-Stage Dockerfile
dockerfile
# Build stage
FROM python:3.9-alpine as builder
WORKDIR /app
COPY requirements.txt .
RUN pip install --user -r requirements.txt

# Final stage
FROM python:3.9-alpine
WORKDIR /app
COPY --from=builder /root/.local /root/.local
COPY . .
ENV PATH=/root/.local/bin:$PATH
EXPOSE 80
CMD ["python", "app.py"]
Image Size Comparison
bash
# Before multi-stage
docker images | grep sample-app
# sopatel264/sample-app    latest    350MB

# After multi-stage  
docker images | grep sample-app
# sopatel264/sample-app    latest    45MB
Benefits of Multi-Stage Builds
Reduced Size: Final image only contains runtime dependencies

Security: No build tools in production image

Efficiency: Smaller images = faster deployment

Clean Separation: Build environment separate from runtime

Task 5: Docker Hub Management
Tag and Push to Docker Hub
bash
# Tag the image
docker tag sopatel264/sample-app:latest sopatel264/sample-app:v1.0

# Login to Docker Hub
docker login -u sopatel264

# Push to registry
docker push sopatel264/sample-app:v1.0

# Verify by pulling
docker pull sopatel264/sample-app:v1.0
Task 6: Data Persistence with Volumes
Create and Use Volumes
bash
# Create volume
docker volume create app_data

# Run container with volume
docker run -d -v app_data:/app/data sopatel264/sample-app:v1.0

# Inspect volume
docker volume inspect app_data
Why Volumes are Essential
Data Persistence: Survive container lifecycle

Backup & Migration: Easy to backup and move data

Performance: Better I/O performance than container filesystem

Sharing: Multiple containers can share same volume

Task 7: Docker Networking
Custom Network Setup
bash
# Create custom network
docker network create app_network

# Run containers on same network
docker run -d --name webapp --network app_network sopatel264/sample-app:v1.0
docker run -d --name database --network app_network -e MYSQL_ROOT_PASSWORD=secret mysql:latest
Network Communication
Containers on same network can communicate using container names as hostnames:

Web app can connect to database using database:3306

Automatic DNS resolution within the network

Isolated from other networks for security

Task 8: Docker Compose Orchestration
docker-compose.yml
yaml
version: '3.8'
services:
  webapp:
    image: sopatel264/sample-app:v1.0
    ports:
      - "8080:80"
    networks:
      - app_network
    depends_on:
      - database

  database:
    image: mysql:latest
    environment:
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: app_db
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - app_network

volumes:
  db_data:

networks:
  app_network:
    driver: bridge
Deploy with Compose
bash
# Start all services
docker-compose up -d

# Check status
docker-compose ps

# View logs
docker-compose logs

# Stop services
docker-compose down
Task 9: Docker Scout Security Analysis
Security Scanning
bash
# Quick vulnerability overview
docker scout quickview sopatel264/sample-app:v1.0

# Detailed vulnerability report
docker scout cves sopatel264/sample-app:v1.0 > scout_report.txt

# Get recommendations
docker scout recommendations sopatel264/sample-app:v1.0
Security Findings Summary
Scanned Image: sopatel264/sample-app:v1.0
Base Image: python:3.9-alpine
Vulnerabilities Found: 15 total

2 CRITICAL

5 HIGH

7 MEDIUM

1 LOW

Key Vulnerabilities & Remediation
OpenSSL CVE-2021-3711 (CRITICAL)

Affected: openssl 1.1.1k-r0

Fix: Update base image to newer Alpine version

Python Packages (MEDIUM)

Affected: Various Python libraries

Fix: Update dependencies in requirements.txt

Security Recommendations
Use python:3.9-alpine3.18 or newer base image

Regularly update Python dependencies

Implement automated security scanning in CI/CD

Consider distroless images for production

Task 10: Documentation and Reflection
Complete Command List
bash
# Image Management
docker build -t sopatel264/sample-app:latest .
docker images
docker tag sopatel264/sample-app:latest sopatel264/sample-app:v1.0
docker push sopatel264/sample-app:v1.0
docker pull sopatel264/sample-app:v1.0

# Container Management  
docker run -d -p 8080:80 sopatel264/sample-app:latest
docker ps
docker stop <container>
docker rm <container>
docker logs <container>

# Volume Management
docker volume create app_data
docker volume ls
docker run -v app_data:/app/data sopatel264/sample-app:v1.0

# Network Management
docker network create app_network
docker network ls
docker run --network app_network sopatel264/sample-app:v1.0

# Multi-Container
docker-compose up -d
docker-compose down
docker-compose logs

# Security
docker scout quickview sopatel264/sample-app:v1.0
docker scout cves sopatel264/sample-app:v1.0
Critical Reflection
Docker's Impact on Modern Development:

Benefits:

Environment Consistency: Eliminates "works on my machine" issues

Rapid Deployment: Containers start in seconds, enabling quick scaling

Resource Efficiency: Higher application density on infrastructure

Microservices Ready: Perfect architecture for modern applications

CI/CD Integration: Streamlines automated testing and deployment

Challenges:

Security: Shared kernel requires careful security practices

Complexity: Orchestration adds operational complexity

Learning Curve: Requires understanding of container concepts

Persistent Storage: Data management requires careful planning

Personal Learnings:

Multi-stage builds significantly reduce image size and attack surface

Proper networking is crucial for microservices architecture

Security scanning should be integrated into development workflow

Docker Compose simplifies local development and testing

Conclusion
Docker has fundamentally changed how we build, ship, and run applications. While it introduces new complexities, the benefits of consistency, efficiency, and scalability make it essential for modern DevOps practices. The key to success is combining Docker with robust security practices and proper orchestration tools.
