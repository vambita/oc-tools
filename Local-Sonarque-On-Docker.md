## Setting up SonarQube using Docker

### Pull the image

`docker image pull sonarqube:latest`

### Start your docker instance

`docker container run -d -p 8182:9000 --name sonarqube-local sonarqube:latest`

