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
