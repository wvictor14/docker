```bash
docker build -t victor2wy/rstudio rstudio/
docker run --rm -d -p 8888:8787 -v /workspace:/workspace -e PASSWORD=password victor2wy/rstudio 
```