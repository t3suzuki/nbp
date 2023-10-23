FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

ARG USERNAME=tomoya-s

RUN apt -y update
RUN apt install -y git sudo g++
RUN apt install -y autoconf make cmake
RUN apt install -y libtool
RUN apt install -y libgflags-dev
RUN apt install -y pkg-config
RUN apt install -y python3 python-is-python3 meson python3-pyelftools libnuma-dev openssl libssl-dev uuid-dev libcunit1-dev libaio-dev libncurses-dev


RUN useradd -m $USERNAME
RUN gpasswd -a $USERNAME sudo
RUN echo "${USERNAME}:hogehoge" | chpasswd

USER $USERNAME
RUN git config --global user.email "t3suzuki@ucsd.edu"
RUN git config --global user.name "Tomoya Suzuki"


WORKDIR /home/$USERNAME/
RUN git clone https://github.com/spdk/spdk.git
WORKDIR /home/$USERNAME/spdk
RUN git submodule update --init
RUN ./configure
RUN make

WORKDIR /home/$USERNAME/
RUN git clone -b 6.15.fb https://github.com/spdk/rocksdb.git
WORKDIR /home/$USERNAME/rocksdb
RUN export USE_RTTI=1
RUN make -j 12 db_bench DEBUG_LEVEL=0 SPDK_DIR=../spdk

#scripts/gen_nvme.sh --json-with-subsystems

#HUGEMEM=5120 scripts/setup.sh


