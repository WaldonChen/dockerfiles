FROM ubuntu:18.04
MAINTAINER Waldon Chen "waldonchen@gmail.com"
ENV DEBIAN_FRONTEND noninteractive

## Install prerequisite packages
RUN sed -i 's/archive.ubuntu.com/mirrors.tuna.tsinghua.edu.cn/g' /etc/apt/sources.list
RUN apt-get update && apt upgrade -y
RUN apt-get install -y -q   \
        apt-utils sudo      \
        build-essential     \
        qtcreator           \
        qt5-default

# qt5-doc, qt5-doc-html, qtbase5-doc-html, qtbase5-examples

## Clean
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

## Add user
# Replace 1000 with your user / group id
RUN export uid=1000 gid=1000 && \
    mkdir -p /home/developer && \
    echo "developer:x:${uid}:${gid}:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
    echo "developer:x:${uid}:" >> /etc/group && \
    echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
    chmod 0440 /etc/sudoers.d/developer && \
    chown ${uid}:${gid} -R /home/developer

USER developer
ENV HOME /home/developer

CMD ["/bin/bash"]
