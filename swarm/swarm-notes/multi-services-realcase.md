# Mutli-services app real life scenario

![](./multi-services-realcase-1.png)


Using 3 nodes.

## Networks

- `docker network create -d overlay backend`
- `docker network create -d overlay frontend`


## Services

- `docker service create --name vote -p 80:80 --network frontend --replicas 2 dockersamples/examplevotingapp_vote:before`


- `docker service create --name redis --network frontend --replicas 2 redis:3.2`

- `docker service create --name worker --network frontend --network backend dockersamples/examplevotingapp_worker`

- `docker service create --name db --network backend --mount type=volume,source=db-data,target=/var/lib/postgresql/data -e POSTGRES_PASSWORD=password postgres:9.4`

- `docker service create --name result --network backend -p 5001:80 dockersamples/examplevotingapp_result:before`
