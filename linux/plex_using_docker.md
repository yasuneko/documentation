```
docker run -d \
  --name=plex \
  --net=host \
  -e PUID=1000 \
  -e PGID=1000 \
  -e VERSION=docker \
  -e PLEX_CLAIM= `#optional` \
  --mount type=bind,source=/mnt/sda1/Video/TV_Shows,target=/home/video/tv \
  --mount type=bind,source=/mnt/sda1/Video/Movies,target=/home/video/movie \
  --restart unless-stopped \
  --device=/dev/dri:/dev/dri \
  linuxserver/plex
```