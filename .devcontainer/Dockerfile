FROM ubuntu:20.04

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    build-essential bison flex python3 python3-pip openjdk-8-jre openjdk-8-jdk gradle

ENV JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64/"
RUN update-java-alternatives --set java-1.8.0-openjdk-amd64

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    lsb-release wget software-properties-common gnupg
ADD https://apt.llvm.org/llvm.sh /tmp/llvm.sh
RUN chmod +x /tmp/llvm.sh && /tmp/llvm.sh 14
ENV CLANG_HOME="/usr/lib/llvm-14/"

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    cmake git

ARG USERNAME=user
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Create the user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    #
    # [Optional] Add sudo support. Omit if you don't need to install software after connecting.
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# [Optional] Set the default user. Omit if you want to keep the default as root.
USER $USERNAME
