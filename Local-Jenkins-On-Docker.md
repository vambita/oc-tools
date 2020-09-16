## Setting up Jenkins using Docker

### Pull the image

`docker image pull jenkins/jenkins:latest`

### Create the persistent volume

`docker volume create  jenkins_data`

### Start your docker instance

`docker container run -d -p 8181:8080 -v jenkins_data:/var/jenkins_home --name jenkins-local jenkins/jenkins:latest`