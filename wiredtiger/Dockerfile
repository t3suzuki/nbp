FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

ARG USERNAME=tomoya-s

RUN apt -y update
RUN apt install -y git sudo g++
RUN apt install -y make cmake autoconf libtool
RUN apt install -y python3-dev python-is-python3 swig

RUN python --version
RUN python3 --version


RUN useradd -m $USERNAME
RUN gpasswd -a $USERNAME sudo
RUN echo "${USERNAME}:hogehoge" | chpasswd

USER $USERNAME
RUN git config --global user.email "t3suzuki@ucsd.edu"
RUN git config --global user.name "Tomoya Suzuki"

WORKDIR /home/$USERNAME/
RUN git clone https://github.com/wiredtiger/wiredtiger.git
WORKDIR /home/$USERNAME/wiredtiger
RUN mkdir build
WORKDIR /home/$USERNAME/wiredtiger/build
RUN cmake .. -D CMAKE_BUILD_TYPE=Release
RUN make -j 8

WORKDIR /home/$USERNAME/
RUN git clone https://github.com/t3suzuki/argobots.git
WORKDIR /home/$USERNAME/argobots/
RUN ./build.sh

WORKDIR /home/$USERNAME/
RUN git clone https://github.com/t3suzuki/pthabt.git
