```bash
docker build -t victor2wy/rstudio rstudio/
docker run --rm -p 8888:8787 -e PASSWORD=password victor2wy/rstudio
```