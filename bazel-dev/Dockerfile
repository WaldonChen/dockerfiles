FROM centos:6.6
LABEL version="1.0" maintainer="Waldon Chen <waldonchen@gmail.com>"

## Installing prerequisite packages
RUN yum install -y centos-release-scl
RUN yum install -y devtoolset-7 python27 java-1.8.0-openjdk-devel; yum clean all

ENV BAZEL_VERSION=0.25.3 \
    BAZEL_JAVAC_OPTS="-J-Xmx2g -J-Xms1g" \
    EXTRA_BAZEL_ARGS="--host_javabase=@local_jdk//:jdk"

## Download and extract to /tmp
ADD https://github.com/bazelbuild/bazel/releases/download/${BAZEL_VERSION}/bazel-${BAZEL_VERSION}-dist.zip /tmp/
#COPY bazel-${BAZEL_VERSION}-dist.zip /tmp/
RUN unzip /tmp/bazel-${BAZEL_VERSION}-dist.zip -d /tmp/bazel-${BAZEL_VERSION};

## Build bazel from scratch
RUN cd /tmp/bazel-${BAZEL_VERSION}/; \
    CC="/opt/rh/devtoolset-7/root/usr/bin/gcc" bash ./compile.sh
RUN cp /tmp/bazel-${BAZEL_VERSION}/output/bazel /usr/bin/bazel

## Clean
RUN rm -rf /tmp/* /var/tmp/*
