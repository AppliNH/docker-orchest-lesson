# Updates

When a stack is running, you still can apply some updates to the containers.


### Update the image
`docker service update --image postgres:9.7 <servicename>`

### Adding an env variable
`docker service update --env-add NODE_ENV=product`

### Removing a port
`docker service update --publish-rm 8080`

### Change number of replicas of a service
`docker service scale webapp=6`

*You can do this with two services too*

### From YML file


Just edit the file then 

`docker stack deploy -c stack.yml <sameStackName>`

## Examples

- `docker service create -p 8088:80 --name web nginx:1.13.7`
- `docker service scale web=5`
- `docker service update --image nginx:1.13.6 web`
- `docker service update --publish-rm 8088 --publish-add 9090:80 web`

## Misc

`docker service update --force <serviceName>` will force the update on every nodes