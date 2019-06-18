FROM daocloud.io/waldonchen/qt5-dev:latest
MAINTAINER Waldon Chen "waldonchen@gmail.com"

## Install prerequisite packages
RUN sudo apt-get update \
 && sudo apt-get install -y -q --no-install-recommends \
    wget cmake libexpat1-dev \
    libxerces-c-dev         \
    libmotif-dev            \
    libglw1-mesa-dev        \
    inventor-dev            \
    opticalraytracer        \
    libpythia8-dev          \
    pythia8-doc-html        \
    pythia8-doc-worksheet   \
    pythia8-examples        \
 && sudo apt-get clean      \
 && sudo rm -r /var/lib/apt/lists/*

## Install geant4
WORKDIR /home/developer/
RUN wget http://geant4-data.web.cern.ch/geant4-data/releases/geant4.10.05.p01.tar.gz \
 && tar xf geant4.10.05.p01.tar.gz
RUN mkdir geant4.10.05.p01/build && cd geant4.10.05.p01/build \
 && cmake .. -DGEANT4_INSTALL_DATA=ON \
 -DGEANT4_BUILD_MULTITHREADED=ON -DGEANT4_USE_GDML=ON \
 -DGEANT4_USE_QT=ON -DGEANT4_USE_XM=ON \
 -DGEANT4_USE_OPENGL_X11=ON -DGEANT4_USE_INVENTOR=OFF \
 -DGEANT4_USE_RAYTRACER_X11=ON -DGEANT4_USE_SYSTEM_ZLIB=ON \
 -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr \
 && make -j4 && sudo make install
RUN rm -rf geant4.10.05.p01/

## Clean
RUN sudo rm -rf /tmp/* /var/tmp/*

CMD ["/bin/bash"]
