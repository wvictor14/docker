FROM rocker/rstudio:4.4.0

LABEL source="https://github.com/wvictor14/docker/blob/main/rstudio/Dockerfile"

MAINTAINER Victor Yuan 

ARG bioc_ver=3.19

RUN install2.r -e -s -n -1 \
    devtools 
    
# for theme
# run when rstudio open: `rscodeio::install_theme()`
RUN Rscript -e "remotes::install_github('anthonynorth/rscodeio') 

# regular R package dependencies
RUN install2.r -e -s -n -1 \
    pak \
    readr \
    dplyr \
    tidyr \
    ggplot2 \
    purrr \
    forcats \
    stringr \
    shiny \
    ggh4x \
    here \
    BiocManager \
    && rm -rf /tmp/downloaded_packages
RUN Rscript -e "BiocManager::install(version = '${bioc_ver}')"


# the rstudio/ path is set for building with GitHub Actions
# copies rstudio preferences
COPY --chown=rstudio:rstudio rstudio-prefs.json /home/rstudio/.config/rstudio
COPY --chown=rstudio:rstudio .Rprofile /home/rstudio/

WORKDIR /home/rstudio
