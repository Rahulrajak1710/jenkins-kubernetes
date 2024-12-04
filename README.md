# CI/CD Pipeline Setup with Git, Jenkins, and Kubernetes

## Overview

This repository contains the setup for a Continuous Integration/Continuous Deployment (CI/CD) pipeline using Git, Jenkins, and Kubernetes (K8s). The objective is to automate the process of building artifacts upon code commits to specified Git repositories and deploying them to designated Kubernetes clusters.

## Prerequisites

Before setting up the pipeline, ensure you have the following installed and configured:

- **Git**: Version control system for managing code.
- **Jenkins**: Automation server to handle CI/CD pipelines.
- **Kubernetes (K8s)**: Container orchestration platform for managing applications.
- **kubectl**: Command-line tool to interact with Kubernetes clusters.
- **Docker**: For building and managing container images.
- **GitHub/GitLab**: Repository hosting service (or any other version control system).
- **Jenkins Plugins**:
  - Kubernetes Plugin
  - GitHub Integration Plugin
  - Docker Pipeline Plugin

## Architecture

1. **Git**: Developers push their code changes to the designated Git repository.
2. **Jenkins**: Jenkins monitors the repository for changes, triggers the build pipeline when code is committed, and creates a Docker image of the application.
3. **Kubernetes**: The Docker image is deployed to the appropriate Kubernetes cluster for testing and production.

## Pipeline Workflow

1. **Code Commit**:
   - Developers push code to the Git repository.
   
2. **Build Trigger**:
   - Jenkins is configured to listen for Git commits and triggers the pipeline.
   
3. **Build Stage**:
   - Jenkins fetches the latest code from the repository.
   - Docker image is built using the Dockerfile in the repository.
   
4. **Push Image to Registry**:
   - After building the Docker image, it is pushed to a container registry (e.g., Docker Hub, AWS ECR, Google Container Registry).
   
5. **Deploy to Kubernetes**:
   - Jenkins uses `kubectl` to deploy the newly built Docker image to the Kubernetes cluster.
   - Kubernetes handles scaling, load balancing, and service discovery.

6. **Monitoring**:
   - Jenkins provides logs of the pipeline execution, which can be reviewed for errors and issues.
