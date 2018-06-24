
FROM ubuntu:bionic

FROM python:latest
# Python needs to be before golang otherwise they conflict
FROM golang:latest

RUN apt-get update

RUN apt install -y software-properties-common \
&& apt-get update

RUN wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add -

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 3B4FE6ACC0B21F32

RUN apt-add-repository "deb http://archive.ubuntu.com/ubuntu/ bionic main restricted" 			\
&& apt-add-repository "deb http://apt.llvm.org/bionic/ llvm-toolchain-bionic-6.0 main"	        \
&& apt-get update

RUN apt-get install -y --allow-unauthenticated gcc-7 clang-6.0 lld-6.0 lldb-6.0 vim

RUN ln -s /usr/bin/clang-6.0 /usr/bin/clang 	\
&& ln -s /usr/bin/clang++-6.0 /usr/bin/clang++	\
&& ln -s /usr/bin/lld-6.0 /usr/bin/lld 			\
&& ln -s /usr/bin/lldb-6.0 /usr/bin/lldb

RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash

ENV NVM_DIR /root/.nvm

RUN . $NVM_DIR/nvm.sh 		\
&& nvm install node 		\
&& nvm install --lts 		\
&& nvm install --lts=Boron

ENV GOPATH /home/work

WORKDIR /home/work/

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"

CMD [ "/bin/bash" ]
