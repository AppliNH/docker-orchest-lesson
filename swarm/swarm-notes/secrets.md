# Secrets storage

Easy solution for storing secrets (passwords, TLS certificate and keys, etc).


## How

`docker secret create my_secret my_secret.txt`


you can also go for


`echo "myPasswowrd" | docker secret create pass2 -`

However, both are really secured there :

- The first one creates a file on the disk
- The second can be access through commands history


A good solution would be to use a remote API to register the secret.


`docker secret ls` displays the registered secrets, but without revealing their content of course.


`docker service create --name psql --secret my_secret --secret pass2 -e POSTGRES_PASSWORD_FILE=/run/secrets/my_secret -e POSTGRES_USER FILE=/run/secrets/pass2`


^ Creating a service wich uses the secrets.

