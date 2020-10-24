# This is an auto generated Dockerfile for gazebo:gzweb7
# generated from docker_images/create_gzweb_image.Dockerfile.em
FROM gazebo:libgazebo7-xenial

# install packages
RUN apt-get update && apt-get install -q -y --no-install-recommends \
    build-essential \
    cmake \
    imagemagick \
    libboost-all-dev \
    libgts-dev \
    libjansson-dev \
    libtinyxml-dev \
    mercurial \
    nodejs \
    nodejs-legacy \
    npm \
    pkg-config \
    psmisc \
    xvfb \
    git \
    && rm -rf /var/lib/apt/lists/*

# label gazebo packages
LABEL sha256.libgazebo7-dev=b1aee9ca46363b8b8ae56503af3876466ced9d86b166b69af633204e74317024

# install gazebo packages
RUN apt-get update && apt-get install -y --no-install-recommends \
    libgazebo7-dev=7.16.1-1* \
    && rm -rf /var/lib/apt/lists/*

# clone gzweb
ENV GZWEB_WS /root/gzweb
RUN git clone https://github.com/osrf/gzweb.git $GZWEB_WS
WORKDIR $GZWEB_WS

RUN apt-get update
RUN apt-get install curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt-get install -y nodejs

# build gzweb
RUN git checkout gzweb_1.4.0 \
    && xvfb-run -s "-screen 0 1280x1024x24" ./deploy.sh -m

# setup environment
EXPOSE 8080
EXPOSE 7681

# run gzserver and gzweb
CMD gzserver --verbose & npm start
