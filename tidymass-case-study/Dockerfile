FROM jaspershen/tidymass:latest
MAINTAINER "Xiaotao Shen" shenxt1990@outlook.com

RUN apt-get update && apt-get install -y curl

## RUN R -e 'install.packages("usethis")'

COPY .Renviron /root/.Renviron

COPY case_study/ /home/rstudio/case_study/

RUN chmod -R 777 /home/rstudio/case_study/

RUN R -e 'install.packages("shadowtext")'




