# Docker Tutorial
Docker sample application created using tutorial on https://docs.docker.com/get-started/

To initialize the app:
* install Docker Community Edition from https://docs.docker.com/install/#supported-platforms
* sign up for Docker account to host image repo at https://hub.docker.com/
* install Oracle VirtualBox at https://www.virtualbox.org/wiki/Downloads to run image on virtual machines
* run these commands:

```
docker build -t <image-name-here> .
docker tag <image-name-here> <username-here>/<repository-here>:<tag-here>
```

where the username is predetermined by the account created and the repository, tag and image names are all created within the commands

```
docker push <username-here>/<repository-here>:<tag-here>
```

in the docker-compose.yml file change the "image" attribute to represent the name of your username, repo, and image

```
docker-machine create --driver virtualbox myvm1 
docker-machine create --driver virtualbox myvm2
```

This creates two virtual machines to use as a test cluster for running your images in a "swarm"

```
docker-machine ssh myvm1 "docker swarm init --advertise-addr <myvm1 ip>"
```

Follow instructions from command to add myvm2 as a "worker" in the swarm making sure to use port 2377 instead of 2376
To run commands from the swarm "manager" myvm1, use the commands:

```
docker-machine env myvm1
eval $(docker-machine env myvm1)
```

To deploy the app to the cluster run:
```
docker stack deploy -c docker-compose.yml getstartedlab
```

To view your application run:

```
docker-machine ls
```

and go to the ip address of one of your virtual machines. 
