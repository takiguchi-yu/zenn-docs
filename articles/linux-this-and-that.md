---
title: "Linuxãããã"
emoji: "ð"
type: "idea" # tech: æè¡è¨äº / idea: ã¢ã¤ãã¢
topics: ["linux"]
published: false
---

# ãã¦ã³ãç¶æ³ãè¡¨ç¤º

cat /etc/fstab

# ã¹ã¯ãããã¿ã

cat /proc/swaps

# sjis ã«å¤æ
nkf -s --overwrite

# ãã¡ã¤ã«æ°ã«ã¦ã³ã
ls -laR /home/www/hoge | grep -c '^-'

## ç°¡æç(ãã¡ã¤ã«æ°ããã£ããèª¿ã¹ã)
df -i

# 2ã¤ã®ãã¡ã¤ã«ãæ¯è¼

vim -d A.txt B.txt

# maillogããç¹å®ã®toãã«ã¦ã³ã

grep ã¡ã¢ã -A5 /var/log/maillog | grep "to=" | awk '{print $7}' | sort | uniq -c 

# ãªãã¤ã¬ã¯ãåãåå¾ãã curl 

curl -w "%{redirect_url}" -o /dev/null -s https://ã

# ç´åã®ã³ãã³ããå¼æ°ãä½¿ãå ´å

!$

# ãããã¯ã¼ã¯ç¶æ³

watch --interval=1 "netstat -an | grep 8436 | grep ESTABLISHED"

ESTABLISHEDã»ã»ã»æ¥ç¶ãç¢ºç«ããã¦ç¾å¨éä¿¡ãè¡ããã¦ããç¶æ
TIME_WAITã»ã»ã»æ¥ç¶çµäºå¾ã¡ç¶æã§ãã°ããããã¨CLOSEDã¸ç§»è¡ãã

# 1ç§ééã§ãµã¼ãã¼ãªã½ã¼ã¹ãã¿ã¼ããã«åºåï¼ç¾å¨æå»ä»ãï¼

vmstat 1 | awk '{print strftime("%y/%m/%d %H:%M:%S"), $0}'

# ç¾å¨ã®ãã¦ã³ããã¤ã³ããããªã¼ç¶ã§åºå

findmnt
# ãªã¹ãè¡¨ç¤º
findmnt -l

# ãã£ã¬ã¯ããªã®ãµã¤ãº(å®¹é)ãèª¿ã¹ã
æå¾ã«æ°å¤ã§éé ã«ä¸¦ã¹æ¿ã

du -h --max-depth=1 /db | sort -nr

du -h --max-depth=1 /db

du -ah ./ | sort -rh | head -5

# zcat
zcat /home/log/application_2099????.log.*.gz | grep error

# zgrep 
zgrep -in error /home/log/application_2099????.log.*.gz

# less è¡ã¸ã£ã³ãã
æ°å­+g
300g

# tcpdump
```
sudo tcpdump -i eth0 -w tcpdump-host-%Y%m%d-%H.pcap -G 3600 \( tcp port 9160\) or \( tcp port 7000 \)
nohup sudo tcpdump -i eth0 -w tcpdump-host-%Y%m%d-%H.pcap -G 3600 \( tcp port 9160\) or \( tcp port 7000 \) > /dev/null 2>&1 &
```
åè  
https://milestone-of-se.nesuke.com/sv-basic/linux-basic/tcpdump/  
https://milestone-of-se.nesuke.com/knowhow/tcpdump-command-generator/

# dstat
```
dstat -tamsl -D {ããã¤ã¹(e.g. xvda1)}
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
