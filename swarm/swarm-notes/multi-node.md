# Multi-nodes with SWARM

3 nodes on 3 different machines.

- `docker swarm init --advertise-addr 192.168.0.8`

On the machine you want to be the leader.
Then on the two other machines :

`docker swarm join --token TOKEN_GIVEN_BY_THE_FIRST_MACHINE 192.168.0.8:2377`

You can get the token at any time on the leader machine by using `docker swarm join-token manager`.

So, from the node that has been created, save the token in a variable with something like :


```bash
TOKEN=$(ssh $MASTER_IP docker swarm join-token -q manager)
```




Thanks to `docker node ls` on the leader machine, we can see the two other nodes.

The two other nodes are considered as workers, and won't be able to run swarm commands until they leave the swarm by using `docker leave swarm --force`.

However, you can update the role of a node, using `docker node update --role manager [nodeName]` on the leader node.

The target node will not become a leader tho.

## Creating a service

`docker service create --replicas 3 alpine ping 8.8.8.8` will create a service replicated 3 times.


With the command `docker node ps node3` or `node2` or `node1` we can see that each of the node has a replication of this service.


Here you go. This is a fully operationnal Swarm cluster.