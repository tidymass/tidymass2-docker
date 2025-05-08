# FROM yufree/xcms:latest
FROM --platform=linux/amd64 bioconductor/bioconductor_docker:RELEASE_3_16
# MAINTAINER "Xiaotao Shen" xiaotao.shen@outlook.com
LABEL maintainer="Xiaotao Shen <xiaotao.shen@outlook.com>"

# RUN apt-get update && apt-get install -y curl
RUN apt-get update && apt-get install -y curl libcurl4-openssl-dev libssl-dev libxml2-dev git

## RUN R -e 'install.packages("usethis")'

COPY .Renviron /root/.Renviron

COPY demo_data/ /home/rstudio/demo_data/

RUN chmod -R 777 /home/rstudio/demo_data/

RUN chmod -R 777 /home/rstudio/demo_data

RUN R -e "if (!requireNamespace('BiocManager')) install.packages('BiocManager')"

RUN R -e "BiocManager::install(c('xcms', 'MSnbase'))"

RUN R -e 'install.packages("remotes")'

RUN R -e "remotes::install_gitlab(repo = 'tidymass/massdataset')"

RUN R -e "remotes::install_gitlab(repo = 'tidymass/tidymass', dependencies = TRUE)"



