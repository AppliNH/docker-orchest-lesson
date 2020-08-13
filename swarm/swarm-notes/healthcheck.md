# Healthcheck

The healthcheck command will expect 0 (ok) or 1 (nok) (or else it means an error has occured).


Three states: starting, healthy, unhealthy.


Healthcheck status shows up in `docker container ls`. To check the health status of a specific container, you can user `docker container inspect` which will show the last 5 healthchecks.

**Parameters:**
- `timeout` is the given time to obtain a answer when the health command is executed. Passed the `timeout`, the check is considered as failed.
- `retries` is the number of retries if the command fails.
- `interval` is the interval of time between healthcheck command execution.
- `start-period` is the time after which the healthcheck will give healthy/unhealty results. By default it's 30s, but you can set it to 15s for example if you know that a certain service takes up to 15s to start. Healthcheck will still perform, but the results will be ignored.

## In a DockerFile

You can already set an healthcheck command in a Dockerfile.

Example :

`HEALTHCHECK curl -f http://localhost/ || false `

*(here the `|| false` allows the command to simply return 1 if the result isn't 0)*

or

`HEALTHCHECK --interval=30s --timeout=3s --retries=3 --start-period=20s CMD curl -f http://localhost/ || exit 1`

*(`exit 1` here is the same as `false`)*

