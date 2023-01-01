---
title: "AmazonLinux2"
emoji: "🙆"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["docker"]
published: false
---

AWS を使っていると何かと Amazon Linux がほしくなるときがあるため、その開発環境を Dockerイメージ で用意し、Visual Studio Code (VSCode) から接続して使ってみます。

やることは以下になります。DockerのインストールやVSCodeのインストールは割愛します。

* Dockerイメージ作成
  * python
* VSCodeからDockerイメージに接続

# 環境

* MacOS

# Dockerイメージ作成

```Dockerfile
FROM amazonlinux:2
# Or command: docker run -it --rm --name amazonlinux2 -v ~/.aws:/root/.aws amazonlinux:2 bash

# install amazon-linux-extras install
RUN amazon-linux-extras install -y

# yum update & install
RUN yum update -y \
    && yum install -y \
        systemd \
        tar \
        unzip \
        sudo

# install aws cli v2
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
    && unzip awscliv2.zip \
    && sudo ./aws/install

# create user
RUN useradd "ec2-user" && echo "ec2-user ALL=NOPASSWD: ALL" >> /etc/sudoers

# install for develop, etc.
RUN sudo amazon-linux-extras install -y \
    golang1.11 \
    python3.8

# init
CMD ["/sbin/init"]
```

# docker-compose.yml作成

```yml
version: '3'
services:
  amazonlinux:
    container_name: mydev
    build: 
      context: .
    command: /bin/bash
    tty: true
    volumes:
      - ./tmp:/var/tmp


version: "3.7"

services:
  amazonlinux2:
    build: .
    container_name: amazonlinux2
    privileged: true
    restart: always
    volumes:
      - type: bind
        source: ./share
        target: /share
      - type: bind
        source: ~/.aws
        target: /home/ec2-user/.aws
```

コンテナを起動

```
$ docker-compose up --build
```

```
$ docker exec -it amazonlinux2 bash
$ su - ec2-user
$ aws --version
```


# VSCodeから接続

* https://dev.classmethod.jp/articles/amazon-linux-2-docker-aws-cli-visual-studio-code/
