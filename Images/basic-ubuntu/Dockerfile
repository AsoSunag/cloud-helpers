
FROM ubuntu:bionic

FROM python:latest
# Python needs to be before golang otherwise they conflict
FROM golang:latest

RUN apt-get update

RUN apt install -y software-properties-common \
&& apt-get update

RUN wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add -

RUN apt-add-repository "deb http://archive.ubuntu.com/ubuntu/ bionic main restricted" 								\
&& apt-add-repository "deb http://archive.ubuntu.com/ubuntu/ bionic-updates main restricted" 						\
&& apt-add-repository "deb http://archive.ubuntu.com/ubuntu/ bionic universe"										\
&& apt-add-repository "deb http://archive.ubuntu.com/ubuntu/ bionic-updates universe"								\
&& apt-add-repository "deb http://archive.ubuntu.com/ubuntu/ bionic multiverse"										\
&& apt-add-repository "deb http://archive.ubuntu.com/ubuntu/ bionic-updates multiverse"								\
&& apt-add-repository "deb http://archive.ubuntu.com/ubuntu/ bionic-backports main restricted universe multiverse"	\
&& apt-add-repository "deb http://security.ubuntu.com/ubuntu/ bionic-security main restricted"						\
&& apt-add-repository "deb http://security.ubuntu.com/ubuntu/ bionic-security universe"								\
&& apt-add-repository "deb http://security.ubuntu.com/ubuntu/ bionic-security multiverse"							\
&& apt-add-repository "deb http://apt.llvm.org/bionic/ llvm-toolchain-bionic-6.0 main"								\
&& apt-get update

RUN apt install -y --allow-unauthenticated gcc-7 clang-6.0 lld-6.0 lldb-6.0 vim

RUN ln -s /usr/bin/clang-6.0 /usr/bin/clang && ln -s /usr/bin/lld-6.0 /usr/bin/lld && ln -s /usr/bin/lldb-6.0 /usr/bin/lldb

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
