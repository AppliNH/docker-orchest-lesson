# Inspect objects
*Let's keep the same cluster as in the [pods-creation chapter](./pods-creation)*.

**Display logs for a pod:**
`kubectl logs deployment/my-apache`
*(You can also add `--follow` to this)*
or
`kubectl logs -l run=my-apache`


**Display events, stats, and other details about a pod:**
`kubectl describe pod/{podName}`


