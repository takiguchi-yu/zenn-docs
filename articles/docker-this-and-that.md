---
title: "Dockerãããã"
emoji: "ð"
type: "idea" # tech: æè¡è¨äº / idea: ã¢ã¤ãã¢
topics: ["docker"]
published: false
---

# åæ­¢ãã¦ããã³ã³ãããããªã¥ã¼ã ããããã¯ã¼ã¯ãã¤ã¡ã¼ã¸ãä¸æ¬åé¤
docker system prune 

# åæ­¢ãã¦ããã³ã³ããããã¹ã¦åé¤(noneã®ã¤ã¡ã¼ã¸ãç¶ºéºã«)
docker container prune

# åæ­¢ãã¦ããã¤ã¡ã¼ã¸ããã¹ã¦åé¤
docker image prune

# ä½¿ããã¦ããªãããªã¥ã¼ã ããã¹ã¦åé¤
docker volume prune

# ã¬ã¤ã¤ã¼ãç¢ºèª
docker history {ã¤ã¡ã¼ã¸å}

# ã¤ã¡ã¼ã¸ãã«ã (ã¤ã¡ã¼ã¸ãä½æ)
docker build -t {ã¤ã¡ã¼ã¸å} {Dockerfileãã¹}

# ã³ã³ããèµ·å
docker run --name {ã³ã³ããå} -it {ã¤ã¡ã¼ã¸å} /bin/bash

# ãã«ãæã«ã¤ã¡ã¼ã¸åãã¤ãã
docker build -t cnetos_php53:1.0 .

# -p: publishããããã¹ãã®ãã¼ã8080 ã ã³ã³ããã®ãã¼ã 80 ã«ãã¤ã³ãï¼å²ãå½ã¦ï¼ãã¾ãã
# -d: ããã¯ã°ã©ã¦ã³ãã§èµ·å
docker run -p 8081:80 -d cnetos_php53:1.0
docker run -d cnetos_php53:1.0

# ã³ã³ãããèµ·åãã¦ãããã¨ãç¢ºèª
docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
a9337cd1cef7     

# docker-compose ã§ã¤ã¡ã¼ã¸ããã«ããç´ãã¦èµ·å
docker-compose up --build

# docker-compose å®å¨ã¯ãªã¼ã³ã³ãã³ã
docker-compose down --rmi all --volumes --remove-orphans

# ã³ã³ããåé¤
docker rm {ã³ã³ããID}
# ã³ã³ããå¼·å¶åé¤
docker rm -f {ã³ã³ããID}

# Amazon Linux ãä½¿ãã¨ã

docker run -it --rm --name myamazonlinux -v ~/.aws:/root/.aws amazonlinux:latest bash

# ã­ã¼ã«ã«ã§ä½æä¸­ã®Dockerã¤ã¡ã¼ã¸ã«å¥ã
## ã¯ããã«ã¿ã°ãåã
docker build . -t {ã¿ã°å}
## åã£ãã¿ã°ã«å¥ã
docker run -it --rm {åã£ãã¿ã°å} bash
