```bash
docker build -t victor2wy/rstudio rstudio/

port=8888
container_name=rstudio_server
r_package_dir=/home/vyuan/packages/
rstudio_image=victor2wy/rstudio
docker run --rm \
   -p ${port}:8787 \
   -d \
   --name ${container_name} \
   -v ${r_package_dir}:/packages \
   #mount other dirs \
   -e PASSWORD=password \
   $rstudio_image
```