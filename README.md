```bash
docker build -t victor2wy/rstudio rstudio/

# run interactive from local
docker run --rm -it -p 8888:8787 -v /workspace:/workspace -e PASSWORD=password victor2wy/rstudio bash

# run latest from docker hub
docker run --rm -d -p 8888:8787 -v /workspace:/workspace -e PASSWORD=password victor2wy/rstudio:latest
```