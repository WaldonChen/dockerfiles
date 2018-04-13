FROM hub.c.163.com/public/ubuntu:16.04-tools
MAINTAINER Waldon Chen <waldonchen@gmail.com>
ENV GROMACS_VERSION 5.1
RUN apt-get update && apt-get install -y    \
        build-essential cmake libfftw3-dev  \
        libblas-dev liblapack-dev mpich     \
    && rm -rf /var/lib/apt/lists/*
EXPOSE 22
WORKDIR "/"
CMD ["/usr/bin/supervisord"]
