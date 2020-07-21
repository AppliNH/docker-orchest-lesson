# Networking features

`--driver overlay` will allow to create a network where nodes can reach each other, just like a VLAN. It's the kind of driver you'll want to work with while using Swarm.

It is also possible to enable IPSec encryption on network creation.

Something cool is to separate the back-end network from the fornt-end network.

**Note that a service CAN be attached to many different networks at once.**

## Practice

- `docker network create --driver overlay boi`



- `docker service create --name psql --network boi -e POSTGRES_PASSWORD=mypass postgres` inits a service with a postgres db.

It will start on a certain node.

- `docker service create --name drupal --network boi -p 80:80 drupal`


So now, from the node with service named `drupal`, we can talk to the other node where the service named `psql` is running. To access the host, you can use `psql` as the hostname :)

However, the drupal interface is also accessible from other nodes' IP.. How ? Have a look at the [routing mesh](./routing-mesh.md)