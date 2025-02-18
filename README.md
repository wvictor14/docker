```
docker build -t victor2wy/rstudio rstudio/

# interactive, enter zsh
docker run --rm -it -p 8888:8787 -v /home/vyuan/workspace:/workspace -e PASSWORD=password victor2wy/rstudio zsh

# non-interactive
docker run -d --name rstudio2 -p 8887:8787 -v /home/vyuan/workspace:/home/rstudio/workspace -e PASSWORD=password victor2wy/rstudio:latest

# add packages
docker run -d -p 8888:8787 \
  -v /workspace:/home/rstudio/workspace \
  -v /home/vyuan/r_packages/:/packages \
  -e PASSWORD=password \
  victor2wy/rstudio:latest


# run in rstudio
rscodeio::install_theme()
```
