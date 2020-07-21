# Swarm

Simple and easy to use, covers up to 80% of use cases with 20% of Kubernetes functionalities (approximative numbers, just a feeling/idea).

## `docker swarm init`

- Inits Swarm
- Root signing certificate for the whole Swarm
- Certificate for the first node manager
- Join tokens creation (will allow other nodes to join this swarm using this token).
- Creates Raft database to ensure consistency between nodes


There can only be one leader node at the time. You can list nodes using `docker node ls`.


## `docker service create`

Will create a service and returns the service ID.

`docker service ls` allows to list all running services.

The "REPLICAS" column means : 
`[number actually running]/[number you planned on running]`.


`docker service ps [serviceName]` allows you to list the containers (as well as their state) attached to the service.

It also allows to see the history of containers, see if one has crashed for example.

However, if anything crashes, Swarm will try to recovers the container which has crashed.

## `docker service update [serviceName]`

This allows to scale a service up, by changing an attribute.
This won't stop the service tho.


**Example:** 
`docker service update ecstatic_shockley --replicas 3 ` Changes the replicas of the service to 3.

## `docker service rm [serviceName]`

Will remove the service.

