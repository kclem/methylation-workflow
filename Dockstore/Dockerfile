FROM openjdk:8-jre-slim

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

RUN apt-get update \
  && apt-get install -y curl \
  && mkdir -p ~/bin \
  && curl -L -o ~/bin/dockstore https://github.com/ga4gh/dockstore/releases/download/1.6.0/dockstore \
  && chmod +x ~/bin/dockstore \
  && echo 'export PATH=~/bin:$PATH' >> ~/.bashrc

RUN source ~/.bashrc \
  && mkdir -p ~/.dockstore \
  && printf "token: dummy-token\nserver-url: https://dockstore.org/api\n" > ~/.dockstore/config

RUN apt-get install -y python3-pip \
  && curl -o requirements.txt "https://dockstore.org/api/metadata/runner_dependencies?client_version=1.6.0&python_version=3" \
  && pip3 install -r requirements.txt

#install docker
RUN apt-get install -y apt-transport-https ca-certificates gnupg-agent software-properties-common \
  && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - \
  && add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable" \
  && apt-get update \
  && apt-get install -y docker-ce docker-ce-cli containerd.io

RUN export DOCKSTORE_ROOT=T

#RUN dockerd &> /dev/null
