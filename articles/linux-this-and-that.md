---
title: "Linuxあれこれ"
emoji: "🌊"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["linux"]
published: false
---

# マウント状況を表示

cat /etc/fstab

# スワップをみる

cat /proc/swaps

# sjis に変換
nkf -s --overwrite

# ファイル数カウント
ls -laR /home/www/hoge | grep -c '^-'

## 簡易版(ファイル数をざっくり調べる)
df -i

# 2つのファイルを比較

vim -d A.txt B.txt

# maillogから特定のtoをカウント

grep メアド -A5 /var/log/maillog | grep "to=" | awk '{print $7}' | sort | uniq -c 

# リダイレクト先を取得する curl 

curl -w "%{redirect_url}" -o /dev/null -s https://〜

# 直前のコマンドを引数を使う場合

!$

# ネットワーク状況

watch --interval=1 "netstat -an | grep 8436 | grep ESTABLISHED"

ESTABLISHED・・・接続が確立されて現在通信が行われている状態
TIME_WAIT・・・接続終了待ち状態でしばらくするとCLOSEDへ移行する

# 1秒間隔でサーバーリソースをターミナル出力（現在時刻付き）

vmstat 1 | awk '{print strftime("%y/%m/%d %H:%M:%S"), $0}'

# 現在のマウントポイントをツリー状で出力

findmnt
# リスト表示
findmnt -l

# ディレクトリのサイズ(容量)を調べる
最後に数値で降順に並べ替え

du -h --max-depth=1 /db | sort -nr

du -h --max-depth=1 /db

du -ah ./ | sort -rh | head -5

# zcat
zcat /home/log/application_2099????.log.*.gz | grep error

# zgrep 
zgrep -in error /home/log/application_2099????.log.*.gz

# less 行ジャンプ　
数字+g
300g

# tcpdump
```
sudo tcpdump -i eth0 -w tcpdump-host-%Y%m%d-%H.pcap -G 3600 \( tcp port 9160\) or \( tcp port 7000 \)
nohup sudo tcpdump -i eth0 -w tcpdump-host-%Y%m%d-%H.pcap -G 3600 \( tcp port 9160\) or \( tcp port 7000 \) > /dev/null 2>&1 &
```
参考  
https://milestone-of-se.nesuke.com/sv-basic/linux-basic/tcpdump/  
https://milestone-of-se.nesuke.com/knowhow/tcpdump-command-generator/

# dstat
```
dstat -tamsl -D {デバイス(e.g. xvda1)}
dstat -tamsl -D xvda1

nohup dstat -tamsl -D xvda1 --output dstat-`date +%Y%m%d-%H`.csv 5 > /dev/null 2>&1 &
dstat -tamsl -D xvdal
dstat -Tamsl -D xvdal

dstat -Tamsl -D xvda1 --output dstat-`date +%Y%m%d-%H%M`.csv

nohup dstat -Tamsl --noheder --output dstat.csv > /dev/null 2>&1 &

```
https://orebibou.com/2016/06/dstat%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E3%81%A7%E8%A6%9A%E3%81%88%E3%81%A6%E3%81%8A%E3%81%8D%E3%81%9F%E3%81%84%E4%BD%BF%E3%81%84%E6%96%B96%E5%80%8B/

# jstat
```
```

# gzip
```
gzip
```
