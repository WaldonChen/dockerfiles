FROM centos:6.6
MAINTAINER Waldon Chen "waldonchen@gmail.com"

## Installing prerequisite packages
RUN yum install -y centos-release-scl
RUN yum install -y devtoolset-7 python27 java-1.8.0-openjdk-devel; yum clean all

RUN scl enable devtoolset-7 bash

ENV BAZEL_VERSION 0.25.2
ENV BAZEL_JAVAC_OPTS="-J-Xmx2g -J-Xms1g"
ENV EXTRA_BAZEL_ARGS="--host_javabase=@local_jdk//:jdk"

ADD https://github.com/bazelbuild/bazel/releases/download/0.25.2/bazel-${BAZEL_VERSION}-dist.zip /tmp/
RUN unzip /tmp/bazel-${BAZEL_VERSION}-dist.zip -d /tmp/bazel-${BAZEL_VERSION}; cd /tmp/bazel-${BAZEL_VERSION}/; \
        bash ./compile.sh
