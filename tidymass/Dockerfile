# Use rocker/rstudio base image with R 4.4.2
FROM rocker/rstudio:4.4.2

# Metadata
LABEL maintainer="Xiaotao Shen <xiaotao.shen@outlook.com>"

# Build arguments for mirrors
ARG CRAN_MIRROR=https://mirrors.tuna.tsinghua.edu.cn/CRAN/
ARG BIOC_MIRROR=https://mirrors.westlake.edu.cn/bioconductor

# Install system dependencies as root
USER root
RUN apt-get update && apt-get upgrade -y && apt-get install -y --no-install-recommends \
    gfortran \
    libcurl4-openssl-dev \
    libssh2-1-dev \
    libgit2-dev \
    libpng-dev \
    libjpeg-dev \
    libtiff-dev \
    libcairo2-dev \
    libharfbuzz-dev \
    libfribidi-dev \
    zlib1g-dev \
    libbz2-dev \
    liblzma-dev \
    libnetcdf-dev \
    libxml2-dev \
    libjson-c-dev \
    libssl-dev \
    libfontconfig1-dev \
    libfreetype6-dev \
    libicu-dev \
    libhdf5-dev \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Switch to rstudio user for R package installations
USER rstudio
WORKDIR /home/rstudio

# Set CRAN and Bioconductor mirrors
RUN R -e "options(repos = c(CRAN = 'https://mirrors.tuna.tsinghua.edu.cn/CRAN/'))"
RUN R -e "options(BioC_mirror = 'https://mirrors.westlake.edu.cn/bioconductor')"

# Install R packages from CRAN
RUN R -e "install.packages(c('tidyverse', 'writexl','ComplexUpset','plotly', 'BiocManager','devtools'), dependencies = TRUE)"

# Install Bioconductor packages
RUN R -e "BiocManager::install(c('preprocessCore', 'impute', 'mzR', 'MSnbase', 'Rdisop', 'BiocGenerics', 'KEGGREST', 'DelayedArray', 'S4Arrays', 'GenomicRanges', 'multtest', 'MassSpecWavelet', 'xcms', 'Biobase', 'AnnotationFilter'), update = FALSE)"
RUN R -e "install.packages('devtools')"
# Install tidymass packages from GitLab
RUN R -e "devtools::install_gitlab('tidymass/masstools', dependencies = TRUE)"
RUN R -e "devtools::install_gitlab('tidymass/massqc', dependencies = TRUE)"
RUN R -e "devtools::install_gitlab('tidymass/massdataset', dependencies = TRUE)"
RUN R -e "devtools::install_gitlab('tidymass/metid', dependencies = TRUE)"
RUN R -e "devtools::install_gitlab('tidymass/metpath', dependencies = TRUE)"
RUN R -e "devtools::install_gitlab('tidymass/massstat', dependencies = TRUE)"
RUN R -e "devtools::install_gitlab('tidymass/massprocesser', dependencies = TRUE)"
RUN R -e "devtools::install_gitlab('tidymass/massdatabase', dependencies = TRUE)"
RUN R -e "devtools::install_gitlab('tidymass/tidymass', dependencies = TRUE)"

# Install tidymass package from GitHub
RUN R -e "devtools::install_github('tidymass/massdbbuildin', dependencies = TRUE)"

# Expose RStudio Server port
EXPOSE 8787

# Set environment variables for RStudio
ENV RSTUDIO_WWW_PORT=8787
ENV RSTUDIO_WWW_ADDRESS=0.0.0.0
ENV USER=rstudio
ENV HOME=/home/rstudio

# Start RStudio Server
CMD ["/init"]