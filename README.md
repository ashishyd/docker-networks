To connect to local database running on host machine use `host.docker.internal` as address

To create second container for example mongodb, you can use `docker run -d --name=mongodb mongo`

To get ip address of the container, which can be used for container communication use the inspect command `docker container inspect mongodb`.

Alternatively, you can create network

`docker network create favorites-net`

`docker network ls`

`docker run -d --name mongodb --network favorites-network mongo`

Use the container name as address for network communication
`docker run -p 3000:3000 -d --rm --name favorites --network favorites-net favorites-node`

The driver can be set when a Network is created, simply by adding the --driver option.

`docker network create --driver bridge my-net`

Of course, if you want to use the "bridge" driver, you can simply omit the entire option since "bridge" is the default anyways.

Docker also supports these alternative drivers - though you will use the "bridge" driver in most cases:

*host*: For standalone containers, isolation between container and host system is removed (i.e. they share localhost as a network)

*overlay*: Multiple Docker daemons (i.e. Docker running on different machines) are able to connect with each other. Only works in "Swarm" mode which is a dated / almost deprecated way of connecting multiple containers

*macvlan*: You can set a custom MAC address to a container - this address can then be used for communication with that container

*none*: All networking is disabled.

*Third-party plugins*: You can install third-party plugins which then may add all kinds of behaviors and functionalities

