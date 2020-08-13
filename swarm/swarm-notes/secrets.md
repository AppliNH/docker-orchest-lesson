# Secrets storage

Easy solution for storing secrets (passwords, TLS certificate and keys, etc).


## How

`docker secret create my_secret my_secret.txt`


You can also go for


`echo "myPasswowrd" | docker secret create pass2 -`

However, both aren't really secured :

- The first one creates a file on the disk
- The second can be access through commands history


A good solution would be to use a remote API to register the secret.


`docker secret ls` displays the registered secrets, but without revealing their content of course.


`docker service create --name psql --secret my_secret --secret pass2 -e POSTGRES_PASSWORD_FILE=/run/secrets/my_secret -e POSTGRES_USER FILE=/run/secrets/pass2`


**^ Creating a service wich uses the secrets.**

## In a compose-file


The `secrets` key allows to dispense with the `docker secret create` command.

```YML
version: "3.1" # Needs to be 3.1 to accept secrets

services:
  psql:
    image: postgres
    secrets:
     - secretuser
     - secretpass
    environment:
     POSTGRES_PASSWORD_FILE: /run/secrets/secretpass
     POSTGRES_USER_FILE: /run/secrets/secretuser

secrets:
  secretuser:
    file: ./secretuser.txt
  secretpass:
    file: ./secretpass.txt
```

**^ This is good for development, but for production you'd better use `../stacks/deploy-with-secrets.yml` .

## Docker-compose

`docker-compose exec secretpass cat /run/secrets/secretpass` will allow you to user secret during development, with docker-compose.