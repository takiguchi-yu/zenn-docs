---
title: "Amazon CodeBuild を独自の Docker イメージでビルドする"
emoji: "🍣"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["aws"]
published: false
---

# 概要
Amazon CodeBuild を独自の Docker イメージでビルドする。  
参考: https://docs.aws.amazon.com/ja_jp/AmazonECS/latest/developerguide/docker-basics.html

# 環境
* Ubuntu 最新
* AdoptOpenJDK 11
* Gradle 最新
* Ant 最新
* Maven 最新
* Git 最新

# Docker インストール
Amazon EC2 インスタンスにインストールする。  

インスタンスでインストールされているパッケージとパッケージキャッシュを更新
```bash
sudo yum update -y
```
最新の Docker Community Edition パッケージをインストール
```bash
sudo amazon-linux-extras install docker
```
Docker サービスを開始
```bash
sudo service docker start
```
ec2-user を docker グループに追加すると、sudo を使用せずに Docker コマンドを実行できる
```bash
sudo usermod -a -G docker ec2-user
```
SSH ターミナルを閉じて、再ログイン後、以下のコマンドを実行
```bash
docker info
```
# Docker イメージを作成
Dockerfile を作成  
Dockerfile リファレンス: https://docs.docker.com/engine/reference/builder/
```bash
vi Dockerfile
```

```Dockerfile
FROM ubuntu:latest

# base update
RUN apt-get update && apt-get upgrade -y

# add-apt-repository コマンド追加
RUN apt-get install -y apt-file
RUN apt-file update
RUN apt-file search add-apt-repository
RUN apt-get install -y software-properties-common

# gradle & java リポジトリ追加
RUN add-apt-repository ppa:cwchien/gradle
RUN add-apt-repository ppa:rpardini/adoptopenjdk

# gradle & git & maven & ant インストール
RUN apt-get update && apt-get upgrade -y gradle git maven ant

# AdoptOpenJDK 11 インストール
RUN apt-get install -y adoptopenjdk-11-installer
```
Dockerfile から Docker イメージを作成
```bash
docker build -t java-build .
docker images --filter reference=java-build
```
出力:
```bash
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
java-build          latest              57a862424beb        2 minutes ago       1.37GB
```
Docker コンテナを実行
```bash
docker run -it java-build
```
# イメージにタグを付け、Amazon ECR にプッシュ
java-build イメージを保存する Amazon ECR リポジトリを作成する。
```bash
aws ecr create-repository --repository-name java-build-repository --region ap-northeast-1
```
出力:
```json
{
    "repository": {
        "registryId": "{aws_account_id}", 
        "repositoryName": "java-build-repository", 
        "repositoryArn": "arn:aws:ecr:ap-northeast-1:{aws_account_id}:repository/java-build-repository", 
        "createdAt": 1573310049.0, git merge --allow-unrelated-histories origin/master
        "repositoryUri": "{aws_account_id}.dkr.ecr.ap-northeast-1.amazonaws.com/java-build-repository"
    }
}
```
前のステップの repositoryUri の値で hello-world イメージにタグを付ける。
```bash
docker tag java-build {aws_account_id}.dkr.ecr.ap-northeast-1.amazonaws.com/java-build-repository
```
aws ecr get-login --no-include-email コマンドを実行して、レジストリ用の docker login 認証コマンド文字列を取得する。
```bash
aws ecr get-login --no-include-email --region ap-northeast-1
```
前のステップで返された docker login コマンドを実行する。このコマンドは、12 時間有効な認証トークンを提供する。
```bash
docker login -u AWS -p {JWT形式}== https://{region}.dkr.ecr.ap-northeast-1.amazonaws.com
```

前のステップの値 repositoryUri を使用して、Amazon ECR にイメージをプッシュする。
```bash
docker push {aws_account_id}.dkr.ecr.ap-northeast-1.amazonaws.com/java-build-repository
```
# クリーンアップする
Amazon ECR イメージの試用を終了したら、レポジトリを削除し、イメージストレージに対して料金が発生しないようにする。
```bash
aws ecr delete-repository --repository-name java-build-repository --region ap-northeast-1 --force
```
# Amazon ECR リポジトリを使って CodeBuild からアクセスできるように権限を設定
AWSコンソールで ECR を開き、リポジトリ選択後に左のナビゲーションバーの Permissions から権限を追加する。  
詳しくは以下を参照  
https://docs.aws.amazon.com/ja_jp/codebuild/latest/userguide/sample-ecr.html
