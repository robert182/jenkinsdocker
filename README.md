Installation

#Build the Jenkins BlueOcean Docker Image

docker build -t myjenkins-blueocean:2.332.3-1 .

#Create bridge network

docker network create jenkins

#Run the Container

docker run --name jenkins-blueocean --restart=on-failure --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.332.3-1

#Get the password

docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword

#access the jenkins site

externalipaddress:8080

