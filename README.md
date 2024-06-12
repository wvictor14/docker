```
docker build -t victor2wy/rstudio rstudio/

# interactive, enter zsh
docker run --rm -it -p 8888:8787 -v /workspace:/workspace -e PASSWORD=password victor2wy/rstudio zsh

# non-interactive
docker run -d -p 8888:8787 -v /workspace:/home/rstudio/workspace -e PASSWORD=password victor2wy/rstudio:latest

# run in rstudio
rscodeio::install_theme()
```
