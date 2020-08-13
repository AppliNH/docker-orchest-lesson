# Full lifecycle: Dev, Build and Deploy


The idea is to use a `docker-compose.yml` file and to override it with another compose-file whenever you're in a dev, test, or prod environment.


`docker-compose -f docker-compose.yml -f docker-compose.test.yml -d`


This is the command to override the base file `docker-compose.yml` with the file `docker-compose.test.yml`.


`docker-compose -f docker-compose.yml -f docker-compose.test.yml config`


This command allows us to see the final merged compose-file.

You can also output it to a file, using `> output.yml`.

