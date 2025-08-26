FROM rocker/rstudio:4.5.1

LABEL source="https://github.com/wvictor14/docker/blob/main/rstudio/Dockerfile"
LABEL author="Victor Yuan"

# set up R packages
ARG bioc_ver=3.21
RUN install2.r -e -s -n -1 \
    devtools 

RUN sudo apt update -y & sudo apt install -y libglpk-dev
        
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
    bslib \
    htmltools \
    ggh4x \
    here \
    lubridate \
    gt \
    BiocManager \
    leaflet \ 
    reactable \
    crosstalk \
    curl \ 
    png \ 
    xml2 \
    igraph \
    && rm -rf /tmp/downloaded_packages
RUN Rscript -e "BiocManager::install(version = '${bioc_ver}', update = TRUE, ask = FALSE)"

# install omz
RUN sudo apt update -y 
RUN sudo apt install zsh -y
RUN sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" -y
RUN chsh -s "$(which zsh)"
RUN git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
RUN git clone https://github.com/akarzim/zsh-docker-aliases.git  ~/.oh-my-zsh/custom/plugins/zsh-docker-aliases

COPY --chown=rstudio:rstudio .zshrc /.zshrc

# the rstudio/ path is set for building with GitHub Actions
# copies rstudio preferences
COPY --chown=rstudio:rstudio rstudio-prefs.json /home/rstudio/.config/rstudio
COPY --chown=rstudio:rstudio .Rprofile /home/rstudio/

# environmental variables e.g. RENV cache
COPY --chown=rstudio:rstudio .Renviron /home/rstudio/

WORKDIR /home/rstudio
