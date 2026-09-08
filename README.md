# Payflow-demo# Jenkins Setup

## Overview

Jenkins is an automation server used to implement Continuous Integration and Continuous Deployment (CI/CD).

For the PayFlow project, Jenkins is configured to automatically retrieve the project from GitHub and execute the pipeline defined in the `Jenkinsfile`.

## Jenkins Environment

The Jenkins server is running inside a Docker container.

### Docker Image

```text
jenkins/jenkins:lts
```

### Container Name

```text
jenkins
```

### Ports

```text
8080:8080
50000:50000
```

Jenkins can be accessed through:

```text
http://localhost:8080
```

## Docker Volumes

The Jenkins container uses two Docker volumes:

```text
jenkins_home -> /var/jenkins_home
payflow_site -> /var/payflow-deploy
```

### jenkins_home

The `jenkins_home` volume stores Jenkins data, including:

* Jenkins configuration
* Jobs
* Plugins
* Credentials
* Build history

### payflow_site

The `payflow_site` volume is used as the deployment directory for the PayFlow landing page.

The directory inside the Jenkins container is:

```text
/var/payflow-deploy
```

## GitHub Integration

Jenkins is connected to the PayFlow GitHub repository:

```text
https://github.com/Mercyross/Payflow-demo.git
```

The pipeline uses the `main` branch.

The repository contains:

```text
payflow-demo/
├── index.html
├── Jenkinsfile
└── README.md
```

## Jenkins Pipeline

The Jenkins pipeline is defined in the `Jenkinsfile`.

The pipeline contains four stages:

1. Checkout
2. Build
3. Test
4. Deploy

### Checkout

Retrieves the PayFlow project from GitHub.

### Build

Simulates the build process for the PayFlow landing page.

### Test

Runs placeholder tests for the application.

### Deploy

Copies the landing page into the deployment directory:

```bash
cp index.html /var/payflow-deploy/index.html
```

## CI/CD Workflow

The overall workflow is:

```text
GitHub
   |
   v
Jenkins
   |
   v
Checkout
   |
   v
Build
   |
   v
Test
   |
   v
Deploy
   |
   v
PayFlow Staging
```

## Useful Docker Commands

Check whether Jenkins is running:

```bash
docker ps
```

Start Jenkins:

```bash
docker start jenkins
```

Stop Jenkins:

```bash
docker stop jenkins
```

Restart Jenkins:

```bash
docker restart jenkins
```

View Jenkins logs:

```bash
docker logs jenkins
```

View live Jenkins logs:

```bash
docker logs -f jenkins
```

## Troubleshooting

### Permission denied during deployment

If Jenkins cannot write to `/var/payflow-deploy`, the directory permissions can be corrected with:

```bash
docker exec -u root jenkins chown -R jenkins:jenkins /var/payflow-deploy
```

### Check deployment files

To verify that the landing page was copied successfully:

```bash
docker exec jenkins ls -la /var/payflow-deploy
```

## Conclusion

This Jenkins setup demonstrates a basic CI/CD pipeline using GitHub, Jenkins, Docker, and WSL 2. The configuration automates the process of retrieving, building, testing, and deploying the PayFlow landing page.
