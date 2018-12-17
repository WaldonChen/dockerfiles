FROM ubuntu:latest
MAINTAINER Waldon Chen "waldonchen@gmail.com"
ENV DEBIAN_FRONTEND noninteractive

## Install prerequisite packages
RUN apt-get update
RUN apt-get install -y -q openssh-server \
        make gcc g++ mpich \
        libfftw3-dev libtcl8.6

## Setup ssh server
RUN mkdir /root/.ssh
RUN mkdir /var/run/sshd
RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

## Download and install charm++
ADD http://charm.cs.illinois.edu/distrib/charm-6.5.0.tar.bz2 /opt/
RUN cd /opt/; tar -xf charm-6.5.0.tar.bz2; rm charm-6.5.0.tar.bz2
RUN cd /opt/charm-6.5.0/; \
        ./build charm++ mpi-linux-x86_64 -j8 --with-production

## Clean
RUN apt-get clean && \
        rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

## Start ssh daemon
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
