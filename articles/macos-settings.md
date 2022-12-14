---
title: "Mac Settings"
emoji: "ð¨"
type: "idea" # tech: æè¡è¨äº / idea: ã¢ã¤ãã¢
topics: ["Mac"]
published: true
---

# Mac Settings

## mac ã®ããã±ã¼ã¸ããã¼ã¸ã£ homebrew ãå¥ãã

Homebrewãã¤ã³ã¹ãã¼ã«ãã

https://brew.sh/index_ja.html

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew -v

brew update
brew upgrade  # <--æ´æ°ã®ããformulaãåãã«ããã

# ã¤ã³ã¹ãã¼ã«æ¹æ³
brew install <formula>

# ã¤ã³ã¹ãã¼ã«æ¸ã¿ã®formulaã®ç¢ºèª
brew list

# ã¢ã³ã¤ã³ã¹ãã¼ã«æ¹æ³
brew uninstall <formula>

# ä¸è¦ãªformulaã®åé¤
# -nãã¤ãããã¨ã§æ¶ããããã®ã®ä¸è¦§ãè¡¨ç¤ºã§ãã
brew cleanup

# formulaã®æå ±ãè¦ã
brew info <formula>
```

### è¤æ°ãµã¼ãã«ä¸æ¬ã­ã°ã¤ã³

```bash
brew install csshx

# ä½¿ãæ¹
csshx --login username æ¥ç¶å æ¥ç¶å æ¥ç¶å æ¥ç¶å æ¥ç¶å æ¥ç¶å
```

### WireShark

```bash
brew cask install wireshark

# èµ·å
wireshark
```

ãã£ã«ã¿
```bash
# ãã¹ãã¨ãã­ãã³ã«ã§ãã£ã«ã¿ãããå ´åï¼host=local-biz.gnavi.co.jpããã­ãã³ã«=httpï¼
http.host == local-biz.gnavi.co.jp and http

# IPã¢ãã¬ã¹ã§ãã£ã«ã¿
ip.addr = 192.168.33.30

# æéã§ãã£ã«ã¿
frame.time >= "2020-10-30 21:30:00" and frame.time <= "2020-10-30 21:40:00"

# ç¹å®ã®æå­åã§ãã£ã«ã¿
frame contains "test"
```
https://sugarsugar.conf.jp/wireshark%E3%81%AE%E3%83%95%E3%82%A3%E3%83%AB%E3%82%BF%E3%83%BC

æå»åã jst ã«å¤æ´

![](https://storage.googleapis.com/zenn-user-upload/aae0a8f875c7-20221231.jpg)
![](https://storage.googleapis.com/zenn-user-upload/a1ef95bcb9dd-20221231.png)

### pssh 

è¤æ°ãµã¼ãã«ä¸æ¬ã­ã°ã¤ã³ããã¦ãã¢ãã­ã¥ã¡ã³ããå®è¡

```bash
brew install pssh

# ä½¿ç¨ä¾
pssh -h ~/Desktop/pssh/host.list -i -l ã¦ã¼ã¶ã¼å "ls -l /home" | grep  gc | wc -l
```

### mov -> gif å¤æ

```bash
brew install ffmpeg

# å¤æ
ffmpeg -i hogehoge.mov -r 24 fugafuga.gif

i ... ã¤ã³ããããã¡ã¤ã«
r .... ãã¬ã¼ã ã¬ã¼ãï¼ç§éãã¡ã¤ã«æ°ï¼

# ç¢ºèª
open -a /Applications/Google\ Chrome.app fugafuga.gif

# ãªãµã¤ãºï¼æ¨ªå¹1280ã§ã¢ã¹ãã¯ãæ¯åºå®ï¼
ffmpeg -i a.mov -vf scale=1280:-1 -r 12 a.gif
```

### ã¿ã¼ããã«ã§ json ãæ±ã

```bash
brew install jq

# ããã¥ã¢ã«
https://stedolan.github.io/jq/manual/
# ä½¿ç¨ä¾
https://qiita.com/takeshinoda@github/items/2dec7a72930ec1f658af

# jsonãµã³ãã«
{
  "Contents": [
    {
      "LastModified": "2019-12-02T20:52:11.000Z",
      "ETag": "\"ad23ed62d94f6a83b250a3f99a9908b0\"",
      "StorageClass": "STANDARD",
      "Key": "nas01/rest/img/3b/94/2hc3ey4u0000/t_00ap.jpg_t=1370482199",
      "Size": 30093
    }
  ]
}

jq -r '.Contents[0].Key'

# -r ã¯ãåºåçµæããããã«ã¯ã©ã¼ããé¤å¤
```

### fish shell

```bash
brew install fish

# fishãèµ·å
fish

# fishãè¨­å®
fish_config
```

### gnu-sed

mac æ¨æºã® sed ã¯ BSD sed ã¨è¨ã£ã¦å¾®å¦ã«ä½¿ãç©ã«ãªããªãã®ã§ã linux æ¨æºã® GNU sed ãã¤ã³ã¹ãã¼ã«ãã¦ãã

```bash
brew install gnu-sed
```

### MySQLç¨CLI

```bash
brew update && brew install mycli
```

### æä½ãã¦ããã­ã¼ãç»é¢ã«è¡¨ç¤ºãã

```bash
brew install keycastr --cask
```

### icnsãã¡ã¤ã«ãä½æ

éå¸¸Macã®ã¢ããªã±ã¼ã·ã§ã³ãã³ãã«(.app)ã®ä¸­ã«ã¯ããã®ã¢ããªã®ã¢ã¤ã³ã³ã¨ãã¦ãicnsããã¡ã¤ã«ãæ ¼ç´ããã¦ãã

```bash
$ brew install makeicns
$ makeicns -in icon.png -out icon.icns
```
https://softantenna.com/blog/makeicns/

### colima ï¼DockerDesktop ã®ä»£æ¿ï¼

```bash
brew install colima

# èµ·å
colima start
# ãªãã·ã§ã³ãä»ãã¦èµ·å
colima start --cpu 1 --memory 2 --disk 10
# åæ­¢
colima stop
```
https://github.com/abiosoft/colima

## ãã¹ã¦ã®ã¢ããªã±ã¼ã·ã§ã³ã®å®è¡ãè¨±å¯

ãã¾ã«å¥ããããªãã¢ããªãããã®ã§ä»¥ä¸ã®ã³ãã³ãã§å®è¡ãè¨±å¯ãã

```bash
sudo spctl --master-disable
```

## å¤§æå­å°æå­ãç¡è¦ãã TAB è£å®ãè¨­å®

```bash:.inputrc
# TABè£å®æã«å¤§æå­å°æå­ãç¡è¦
set completion-ignore-case on

# ãã¡ã¤ã«ã¿ã¤ããã«ã©ãã«ã«ãã
set colored-stats on

# TABè£å®ã®æ¥é ­è¾ãã«ã©ãã«ã«ãã
set colored-completion-prefix on

# å®è¡ãã¡ã¤ã«ã«å°ãä»ãã
set visible-stats on

# Bashãviã¢ã¼ãã«ãã
set editing-mode vi

# ââã­ã¼ã§hisotoryããå¥åè£å®ããï¼ä¾ãã°ãcat + âã§éå»ã®cat + XXX ãå¼ã³åºãï¼
"\e[A":history-search-backward  # arrow up
"\e[B":history-search-forward  # arrow down
```

## ã¹ãã¼ãå¼ç¨ç¬¦ããªãã«ãã

![](https://storage.googleapis.com/zenn-user-upload/edf0bbbb6eae-20221231.jpg)
