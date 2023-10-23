FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

ARG USERNAME=tomoya-s

RUN apt -y update
RUN apt install -y git sudo g++
RUN apt install -y autoconf make cmake
RUN apt install -y libtool
RUN apt install -y libgflags-dev


RUN useradd -m $USERNAME
RUN gpasswd -a $USERNAME sudo
RUN echo "${USERNAME}:hogehoge" | chpasswd

USER $USERNAME
RUN git config --global user.email "t3suzuki@ucsd.edu"
RUN git config --global user.name "Tomoya Suzuki"


WORKDIR /home/$USERNAME/
RUN git clone https://github.com/t3suzuki/argobots.git
WORKDIR /home/$USERNAME/argobots/
RUN ./build.sh

WORKDIR /home/$USERNAME/
RUN git clone https://github.com/t3suzuki/pthabt.git


WORKDIR /home/$USERNAME/
RUN git clone https://github.com/facebook/rocksdb.git


WORKDIR /home/$USERNAME/rocksdb
RUN git checkout -b v7.0.2
RUN mkdir build
WORKDIR /home/$USERNAME/rocksdb/build
RUN cmake .. -D CMAKE_BUILD_TYPE=Release -D WITH_FALLOCATE=OFF
RUN make -j 8

