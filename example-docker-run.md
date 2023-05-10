## Docker


### Viewing Container Logs

***Let’s start with a simple container. We’ll create one that prints a message every second.***

```
$ docker run --name test -d busybox sh -c "while true; do $(echo date); sleep 1; done"
```

> This command is an example from the Docker website. It executes a minimal Docker container with a Bourne shell script that logs a timestamp once every second.  

***If there’s too much output for a single screen, pipe it to a buffering command like less.***

```
$ docker logs test | less
```

***But sometimes, you want to follow the logs as the container is running.***

```
$ docker logs --follow test
```

### Redirect Docker Logs to File

***To redirect the current logs to a file, use a redirection operator.***

```
$ docker logs test > output.log
```

***To send the current logs and then any updates that follow,  use `--follow` with the redirection operator.***

```
$ docker logs -f test > output.log
```

***what if you want to keep the logs and view them at the same time?***

> use tee to watch the output and save it to a file at the same time.  

```
$ docker logs -f test |tee output.log
```

***docker inspect***

```
docker inspect --format='{{.LogPath}}' container_name
```

<details open><summary><i>Test:</i></summary><blockquote>

```
docker inspect --format='{{.LogPath}}' es7179-elasticsearch-1
```

<details><summary><i>Response:</i></summary>

```
/var/lib/docker/containers/d1240223d8c4050860a62e57770911efb1935de5cdbe2700f00a4e386d0c43ca/d1240223d8c4050860a62e57770911efb1935de5cdbe2700f00a4e386d0c43ca-json.log
```

</details>

</blockquote></details>


