FROM centos:6.6
LABEL version="1.0" maintainer="Waldon Chen <waldonchen@gmail.com>"

## Installing prerequisite packages
RUN yum install -y centos-release-scl && \
    yum install -y devtoolset-7 python27 rh-git29 \
                   java-1.8.0-openjdk-devel wget tar && \
    yum clean all

ENV BAZEL_VERSION=0.26.1 \
    BAZEL_JAVAC_OPTS="-J-Xmx2g -J-Xms1g" \
    EXTRA_BAZEL_ARGS="--host_javabase=@local_jdk//:jdk"

## Download and extract to /tmp
## Build bazel from scratch
RUN wget https://github.com/bazelbuild/bazel/releases/download/${BAZEL_VERSION}/bazel-${BAZEL_VERSION}-dist.zip -O - | tar xC /tmp && \
    cd /tmp/bazel-${BAZEL_VERSION}/ && \
    source scl_source enable devtoolset-7 python27 rh-git29 && \
    bash ./compile.sh && \
    cp output/bazel /usr/bin/bazel

## Clean
RUN rm -rf /tmp/* /var/tmp/*
