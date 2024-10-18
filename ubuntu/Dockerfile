FROM ubuntu:latest

# Build arguments
ARG UNAME="user"
ARG UID=1337
ARG GID=1337
ARG PASSWD="<openssl passwd>"

# Initial sytem update + upgrade
RUN apt update -y && \
DEBIAN_FRONTEND=noninteractive apt full-upgrade -y  && \
apt autoremove -y && \
apt clean

# Install packages
RUN DEBIAN_FRONTEND=noninteractive apt install -y \
sudo \
unminimize \
man-db \
iproute2 \
tree \
bat \
inetutils-ping \
vim \
git \
wget \
curl \
tmux \
file

RUN DEBIAN_FRONTEND=noninteractive yes | unminimize

# Setup group and user
RUN groupadd -g ${GID} -o ${UNAME}
RUN DEBIAN_FRONTEND=noninteractive useradd \
-u ${UID} \
-g ${GID} \
-o \
-m \
-s /usr/bin/bash \
-G sudo,staff \
-p ${PASSWD} \
${UNAME}

# Set env + user + workdir
ENV TERM=xterm-256color
USER ${UNAME}
WORKDIR /home/${UNAME}
RUN touch .hushlogin

# Setup dotfiles
RUN git clone https://github.com/3faa9516/dotfiles .dotfile && \
cd .dotfiles && \
./setup.sh && \
git checkout linux

ENTRYPOINT ["/usr/bin/bash"]
