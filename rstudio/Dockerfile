FROM rocker/rstudio:4.4.0

LABEL source="https://github.com/wvictor14/docker/blob/main/rstudio/Dockerfile"

MAINTAINER Victor Yuan 

# set up R packages
ARG bioc_ver=3.19
RUN install2.r -e -s -n -1 \
    devtools 
    
# for theme
# run when rstudio open: `rscodeio::install_theme()`
RUN Rscript -e "devtools::install_github('anthonynorth/rscodeio')"

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
    lubridate \
    gt \
    BiocManager \
    leaflet \ 
    reactable \
    crosstalk \
    && rm -rf /tmp/downloaded_packages
RUN Rscript -e "BiocManager::install(version = '${bioc_ver}')"

# install omz
RUN sudo apt update -y 
RUN sudo apt install zsh -y
RUN sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" -y
RUN chsh -s "$(which zsh)"
COPY --chown=rstudio:rstudio .zshrc /.zshrc

# the rstudio/ path is set for building with GitHub Actions
# copies rstudio preferences
COPY --chown=rstudio:rstudio rstudio-prefs.json /home/rstudio/.config/rstudio
COPY --chown=rstudio:rstudio .Rprofile /home/rstudio/

WORKDIR /home/rstudio
