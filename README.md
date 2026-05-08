# Django Microservices Deployment Using Docker Compose

## Overview
This repository contains a solution for the "Lab Manual 2: Django Microservices Deployment Using Docker Compose" exercise. It demonstrates how to create independent Django applications and containerize them using Docker and Docker Compose.

---

## Prerequisites: WSL and Docker Installation (Windows)

Before running the project, you need to ensure that **Windows Subsystem for Linux (WSL)** and **Docker Desktop** are installed and properly configured on your machine.

### 1. Install WSL (Windows Subsystem for Linux)
1. Open PowerShell or Windows Command Prompt as **Administrator**.
2. Run the following command to install WSL and the default Linux distribution (Ubuntu):
   ```bash
   wsl --install
   ```
3. Restart your computer if prompted.
4. After restarting, open the newly installed Ubuntu terminal from your Start Menu to finish setting up your Linux username and password.

### 2. Install Docker Desktop
1. Download **Docker Desktop for Windows** from the [official Docker website](https://www.docker.com/products/docker-desktop/).
2. Run the installer and follow the on-screen instructions.
3. **Important**: During installation, ensure the option **"Use WSL 2 instead of Hyper-V"** is checked.
4. Once installed, launch Docker Desktop.
5. Go to **Settings (gear icon) > Resources > WSL Integration** and make sure "Enable integration with my default WSL distro" is turned on.

---

## Setup Instructions

Once Docker and WSL are running, follow these steps to run the microservices:

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/Zsxcylliope/Lab-Manual-2-Django-Microservices-Deployment-Using-Docker-Compose.git
   cd Lab-Manual-2-Django-Microservices-Deployment-Using-Docker-Compose
   ```

2. **Build and Run Containers**:
   Execute the following command in the root directory to build the images and spin up the containers:
   ```bash
   docker-compose up --build
   ```

3. **Test the Services**:
   Open your browser and navigate to the following URLs to confirm the services are returning JSON responses:
   - **User Service:** [http://localhost:8001/users/](http://localhost:8001/users/)
   - **Product Service:** [http://localhost:8002/products/](http://localhost:8002/products/)

4. **Stop the Services**:
   Press `CTRL + C` in the terminal to stop the containers. To completely remove the containers and clean up the network, run:
   ```bash
   docker-compose down
   ```

---

## Guide Questions & Answers

**1. How does Django support microservices development?**
Django can serve as an independent microservice by exposing RESTful API endpoints (using JsonResponse as seen in this lab, or the Django REST Framework). This allows different Django applications to act as decoupled, independent services that communicate with frontend applications or other backend services using standardized data formats like JSON over HTTP.

**2. What advantages do containers provide for Django deployment?**
Containers package the Django application alongside all its dependencies (like the specific Python version and required packages) into a single, isolated unit. This guarantees that the application will run consistently across any environment (development, staging, or production). It also prevents dependency conflicts between different projects and simplifies the scaling and deployment process.

**3. How would you enable service-to-service communication?**
Service-to-service communication can be achieved over HTTP using libraries such as Python's requests. In a Docker Compose environment, services can reach each other using their service names as hostnames. For example, the user service could make a request to the product service using the internal network URL: http://product-service:8000/products/.

**4. How can this setup be scaled using Kubernetes?**
To scale this setup in Kubernetes, you would:
- Build and push the Docker images for both services to a container registry.
- Write Kubernetes Deployment manifests for each service, allowing you to easily define the number of replicas (instances) you want running to handle more traffic.
- Create Kubernetes Services to provide stable internal IP addresses and DNS names for the pods, enabling them to communicate with one another.
- Use a Horizontal Pod Autoscaler (HPA) to automatically scale the number of pods up or down based on metrics like CPU or memory utilization.
