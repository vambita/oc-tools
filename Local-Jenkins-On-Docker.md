## Setting up Jenkins using Docker

### Build the custom docker image

The custom Jenkins docker image allows running Docker in the Jenkins container so that we docker command to create and publish images.

`docker build --file docker/jenkins-with-docker/Dockerfile --tag vambita/jenkins:latest .`
`docker push vambita/jenkins:latest`

### Create the persistent volume

`docker volume create jenkins_data`

### Start your docker instance

`docker container run -d -p 8181:8080 -v jenkins_data:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock --name jenkins-local jenkins/jenkins:latest`

### Get that initial password

`docker container exec jenkins-local sh -c "cat /var/jenkins_home/secrets/initialAdminPassword"`

### Tail those logs

