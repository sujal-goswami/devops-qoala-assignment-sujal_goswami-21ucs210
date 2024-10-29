# Assignment Report

---

## Overview
This report documents the deployment of an application using Nginx as a reverse proxy to serve a Python Flask application. The deployment is managed through Docker containers, and the complete CI/CD pipeline is automated using GitHub Actions.

---

> **Note**: All screenshots can be found below.

## Issues Identified

### 1. Docker Image Build Errors
   - **Problem**: Typos in Dockerfiles and the `docker-compose.yml` file caused errors during the image build, and `options` in the compose file `networks` also created problems.
   - **Resolution**: Fixed syntax errors, including using correct port numbers as integer and corrected file paths for `nginx.conf` and HTML files.

### 2. Configuration Errors in `nginx.conf`
   - **Problem**: Incorrect configurations in `nginx.conf` (e.g., misspelling the `worker_processes`, `default_type`, `worker_connections` and `mime.types` keywords) and HTML file path problem.
   - **Resolution**: Corrected all keywords and creating HTML file with proper path. This enabled proper connection handling, MIME type support, and routing.

### 3. Zero MAC Address in container application Output
   - **Problem**: The MAC address displayed as `00:00:00:00:00:00` due to container network isolation.
   - **Resolution**: This limitation is due to Docker's virtual network, which restricts access to host MAC addresses.

---

## Resolution Steps

1. **Nginx and Python App Dockerfile Corrections**: 
   - Corrected package incorrect installs, Dockerfile syntax, paths and specifically in the `COPY` commands, `EXPOSE` statements and `CMD` command.
   - Built the images after corrections and confirmed successful build completion.

2. **Configuration Fixes**:
   - Updated `nginx.conf` to properly route requests to the Python app through `proxy_pass`, and fixed syntax errors in worker and connection settings.

3. **Testing and Verification**:
   - Tested the application in a local environment, accessed via `http://localhost:80`, and confirmed successful connection to the Python app.
   - Verified that the Nginx access logs display request entries confirming successful requests to the Flask application.

---

## CI/CD Pipeline

Since cloud services were not used for this project, I developed a full CI/CD pipeline with GitHub Actions to automate the application deployment. The workflow includes:

1. **Build and Push Docker Images**:
   - Builds Docker images for both the Nginx and Python applications.
   - Pushes these images to Docker Hub for version management.

2. **Deploy to VPS**:
   - The CI/CD pipeline connects to the VPS, pulls the latest Docker images from Docker Hub, and deploys them according to the `docker-compose.yml` configuration.
   - Uses inline Docker Compose commands to handle service setup directly, without requiring an uploaded `docker-compose.yml` file.

---

## Screenshots

- **Application Running in Browser and container**:
  
| ![](https://github.com/sujal-goswami/devops-qoala-assignment-sujal_goswami-21ucs210/blob/main/errors_screenshots/Screenshot%202024-10-29%20213952.png) | ![](https://github.com/sujal-goswami/devops-qoala-assignment-sujal_goswami-21ucs210/blob/main/errors_screenshots/Screenshot%202024-10-29%20203417.png) |
| -------------------------------------------------------------------------------------------------------------------------------------------------------| -------------------------------------------------------------------------------------------------------------------------------------------------------|


- **Nginx Access Logs**:

  | ![](https://github.com/sujal-goswami/devops-qoala-assignment-sujal_goswami-21ucs210/blob/main/errors_screenshots/Screenshot%202024-10-29%20213314.png)                     |
  |----------------------|

- **All other errors screenshots can be found here**: [Link](https://github.com/sujal-goswami/devops-qoala-assignment-sujal_goswami-21ucs210/tree/main/errors_screenshots)


---

### Note on Cloud Deployment
Due to limited access to paid cloud services, I was unable to deploy this application on a cloud server. However, the complete deployment process is configured via GitHub Actions to simulate a production environment deployment. This setup ensures the application is containerized, versioned, and easily deployable on any VPS or cloud server if access becomes available. 

---

Thank you for reviewing this Report documentation.
