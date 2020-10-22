FROM ubuntu
USER root
RUN export DEBIAN_FRONTEND=noninteractive
RUN apt-get update
RUN apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
RUN apt-get install -y docker-ce docker-ce-cli containerd.io

# Trust CA for KM C1D environment
COPY ca.crt /usr/local/share/ca-certificates/ca.crt
RUN update-ca-certificates

# Trust docker registries in KM C1D environment
COPY daemon.json /etc/docker/daemon.json

# Set user back to cnb user to lock down image
# USER 1000:1000