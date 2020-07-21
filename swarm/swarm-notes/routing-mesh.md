# Routing Mesh

It's a incoming (ingress) network which distributes packets for a service to proper task.


It balance the loads among all the nodes registered in the swarm.

So every service will be accessible from any node, if the service has enabled port binding.

## Practice

`docker service create --name search --replicas 3 -p 9200:9200 elasticsearch:2`

Then, `curl localhost:9200` will work on every nodes.