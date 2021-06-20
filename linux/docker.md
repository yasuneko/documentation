Error:
```
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post http://%2Fvar%2Frun%2Fdocker.sock/v1.24/images/create?fromImage=linuxserver%2Fplex&tag=latest: dial unix /var/run/docker.sock: connect: permission denied
```

resolve using
```
> sudo chmod 666 /var/run/docker.sock
```

install docker-compose
```
> sudo apt install docker-compose
```