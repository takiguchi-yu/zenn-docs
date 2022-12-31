---
title: "Dockerあれこれ"
emoji: "👋"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["docker"]
published: false
---

# 停止しているコンテナ、ボリューム、ネットワーク、イメージを一括削除
docker system prune 

# 停止しているコンテナをすべて削除(noneのイメージも綺麗に)
docker container prune

# 停止しているイメージをすべて削除
docker image prune

# 使われていないボリュームをすべて削除
docker volume prune

# レイヤーを確認
docker history {イメージ名}

# イメージビルド (イメージを作成)
docker build -t {イメージ名} {Dockerfileパス}

# コンテナ起動
docker run --name {コンテナ名} -it {イメージ名} /bin/bash

# ビルド時にイメージ名をつける
docker build -t cnetos_php53:1.0 .

# -p: publishする。ホストのポート8080 を コンテナのポート 80 にバインド（割り当て）します。
# -d: バックグラウンドで起動
docker run -p 8081:80 -d cnetos_php53:1.0
docker run -d cnetos_php53:1.0

# コンテナが起動していることを確認
docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
a9337cd1cef7     

# docker-compose でイメージをビルドし直して起動
docker-compose up --build

# docker-compose 完全クリーンコマンド
docker-compose down --rmi all --volumes --remove-orphans

# コンテナ削除
docker rm {コンテナID}
# コンテナ強制削除
docker rm -f {コンテナID}

# Amazon Linux を使うとき

docker run -it --rm --name myamazonlinux -v ~/.aws:/root/.aws amazonlinux:latest bash

# ローカルで作成中のDockerイメージに入る
## はじめにタグを切る
docker build . -t {タグ名}
## 切ったタグに入る
docker run -it --rm {切ったタグ名} bash
