# docker-cheatsheet
Purely quicknotes to get started and remember a wide range of collected bits and pieces for docker and some specific images

## pre
run this in console to be able to run docker/docker-compose commands anywhere by adding the default daemon to env
```
eval "$(docker-machine env default)"
```

## Common
start a bash inside the container
```
docker exec -it CONTAINER_NAME /bin/bash
```

display the containers ports forwarded to localhost
```
docker port CONTAINER_NAME
```

display all running containers with ports
```
docker ps
```

execute a command in the container
```
docker exec CONTAINER_NAME <command>
```

kill container immediately
```
docker kill CONTAINER_NAME
```

tries to shutdown the process in the container gracefully then kills it after grace period
```
docker stop CONTAINER_NAME
```

display the ip of the underlying VM where the container resides (machine "default" is useful on a dev host)
```
docker-machine ip MACHINE_NAME
```

forward available ports on host to container ()
```
-P
```

run in background, ensures container is running after run command has been completed
```
-d
```

## Redis
Start a new redis docker container, ensure the folder for data saving exists and write is permitted:
```
docker run --name my-redis -d -p 6379:6379 redis -v /srv/docker/redis:/data --requirepass mysecretpassword --appendonly yes
```

run the redis cli for above
```
docker run -it --link my-redis:redis --rm redis sh -c 'exec redis-cli -h "$REDIS_PORT_6379_TCP_ADDR" -p "$REDIS_PORT_6379_TCP_PORT"'
```

## OrientDB
start the oriented server if not started with the container
```
/usr/local/src/orientdb/bin/server.sh
```

start a container with the latest docker container from the given repo. -d makes sure the container is running after the run command has completed. -P publishes ports to localhost.
```
docker run -d -P --name orientdb -e ORIENTDB_ROOT_PASSWORD=mysecretpassword joaodubas/orientdb:latest
```