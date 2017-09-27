# login into docker-machine hosts default
docker-machine ssh default

# get the IP from your default docker machine
docker-machine ip default

# list
docker-machine ls

# list
docker ps

# bash image
docker exec -it id-name bash

# run image port 49001
docker run -d -p 49001:8080 -v $PWD/jenkins:/var/jenkins_home -t jenkins/jenkins

# stop
docker stop 7db7b29e5b1d

# 
docker-compose -f src/main/docker/cassandra.yml up -d