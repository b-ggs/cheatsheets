# Docker
Containers for days.

## Basic commands
List all running containers
```
docker ps -a
```

Remove all exited containers
```
docker rm $(docker ps --all -q -f status=exited)
```
