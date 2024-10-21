[//]: # (Confidential document)
[//]: # (01/07/2023)
[//]: # (v 1.5.0)


# Docker labs v1.5.0 - Logging

The docker logs command batch-retrieves logs present at the time of execution.

For more information about selecting and configuring logging drivers, refer to Configure logging drivers.

The docker logs --follow command will continue streaming the new output from the container's STDOUT and STDERR.

Passing a negative number or a non-integer to --tail is invalid and the value is set to all in that case.


## Lab 1 : Container logs

- Fetch the logs of a container
- Retrieve logs until a specific point in time (--until). In order to retrieve logs before a specific point in time:

```
docker run --name test-log -d centos:7 sh -c "while true; do $(echo date); sleep 1; done"
date; echo "---"; docker container logs --until=2s test-log
```



