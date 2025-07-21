
[dockerhub](https://hub.docker.com/repository/docker/victor2wy/rstudio/)

```bash
docker build -t victor2wy/rstudio rstudio/

# tag and push
docker tag victor2wy/rstudio victor2wy/rstudio:4.5.1
docker push victor2wy/rstudio:4.5.1

# interactive, enter zsh
docker run --rm -it -p 8888:8787 -v /home/vyuan/workspace:/workspace -e PASSWORD=password victor2wy/rstudio zsh

# non-interactive
docker run -d --name rstudio2 -p 8887:8787 -v /home/vyuan/workspace:/home/rstudio/workspace -e PASSWORD=password victor2wy/rstudio:latest

docker run --name rstudio-d -p 8888:8787 \
  -v /workspace:/home/rstudio/workspace \
  -e PASSWORD=password \
  -e USERID=$UID \ # for non-root
  victor2wy/rstudio:latest

# run in rstudio
rscodeio::install_theme()
```

# renv

To mount a local renv [cache](https://rstudio.github.io/renv/articles/docker.html)

```bash
# the location of the renv cache on the host machine
RENV_PATHS_CACHE_HOST=/home/vyuan/workspace/renv/cache

# where the cache should be mounted in the container
RENV_PATHS_CACHE_CONTAINER=/renv/cache

docker run --rm --name rstudio-v4.5.1 -d -p  8883:8787 \
    -e "RENV_PATHS_CACHE=${RENV_PATHS_CACHE_CONTAINER}" \
    -v "${RENV_PATHS_CACHE_HOST}:${RENV_PATHS_CACHE_CONTAINER}"  \
    -v /home/vyuan/workspace:/home/rstudio/workspace `# mount work directories` \
    -e PASSWORD=password \
    -e USERID=$UID  \
    victor2wy/rstudio:latest
```
