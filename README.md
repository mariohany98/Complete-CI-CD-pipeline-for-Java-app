# Complete CI/CD pipeline for Java-Maven app

This project demonstrates a multi-stage CI/CD pipeline for building and deploying a Java-Maven application. Each stage performs a specific task. Below is a breakdown of what each stage does:

## Stage 1: Increment Version

This stage increments the application version using Maven's build-helper plugin and sets the new version in the pom.xml file.

## Stage 2: Build App

In this stage, the Java application is built using Maven. The 'mvn clean package' command is executed to clean the project

## Stage 3: Build Image

This stage builds a Docker image for the Java application. It uses the previously incremented version and the Jenkins build number to create a unique image tag. The Docker image is built from the application's JAR file and pushed to a Docker Hub repository after logging in with Docker credentials.

## Stage 4: Deploy

In this stage, the previous Docker container is stopped and removed (if it exists), and a new container is started with the latest version of the Java application. 

## Stage 5: Commit Version Update

In the final stage, the changes made to the repository, including the incremented version in the pom.xml file, are committed and pushed to the GitHub repository. Git configuration is set for the Jenkins environment, and the changes are pushed to the main branch of the repository using the provided GitHub token for authentication.

# Prerequisites

1. Install Java Development Kit (JDK).

2. Install Jenkins.

3. Install and configure maven plugin .

4. Install 'credentials binding' plugin and 'credentials' plugin.

5. Define credentials for GitHub and DockerHub on jenkins server.

6. Install docker engine.

7. Allow jenkins user to execute docker commands without using sudo in jenkinsfile.

```bash
sudo usermod -aG docker jenkins
chmod 666 /var/run/docker.sock
systemctl restart jenkins
systemctl restart docker
