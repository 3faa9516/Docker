FROM docker.io/kalilinux/kali-rolling

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

# Install Kali Linux Core
RUN DEBIAN_FRONTEND=noninteractive \
apt install -y kali-linux-core && \
apt update -y

# Install packages
RUN DEBIAN_FRONTEND=noninteractive apt install -y \
man-db \
hydra \
wpscan \
john \
binutils \
zsh \
iproute2 \
tree \
bat \
rlwrap \
inetutils-ping \
vim \
git \
wget \
curl \
file

# Setup group and user
RUN groupadd -g ${GID} -o ${UNAME}
RUN DEBIAN_FRONTEND=noninteractive useradd \
-u ${UID} \
-g ${GID} \
-o \
-m \
-s /usr/bin/zsh \
-G sudo,staff \
-p ${PASSWD} \
${UNAME}

# Set user + workdir
USER ${UNAME}
WORKDIR /home/${UNAME}
RUN touch .hushlogin

# Setup dotfiles
RUN git clone https://github.com/3faa9516/dotfiles .dotfiles && \
cd .dotfiles && \
./setup.sh && \
git checkout linux

ENTRYPOINT ["/usr/bin/zsh"]
