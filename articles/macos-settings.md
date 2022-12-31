---
title: "Mac Settings"
emoji: "💨"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["Mac"]
published: true
---

# Mac Settings

## mac のパッケージマネージャ homebrew を入れる

Homebrewをインストールする

https://brew.sh/index_ja.html

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew -v

brew update
brew upgrade  # <--更新のあるformulaを再ビルドする

# インストール方法
brew install <formula>

# インストール済みのformulaの確認
brew list

# アンインストール方法
brew uninstall <formula>

# 不要なformulaの削除
# -nをつけることで消されるものの一覧を表示できる
brew cleanup

# formulaの情報を見る
brew info <formula>
```

### 複数サーバに一括ログイン

```bash
brew install csshx

# 使い方
csshx --login username 接続先 接続先 接続先 接続先 接続先 接続先
```

### WireShark

```bash
brew cask install wireshark

# 起動
wireshark
```

フィルタ
```bash
# ホストとプロトコルでフィルタをする場合（host=local-biz.gnavi.co.jp、プロトコル=http）
http.host == local-biz.gnavi.co.jp and http

# IPアドレスでフィルタ
ip.addr = 192.168.33.30

# 時間でフィルタ
frame.time >= "2020-10-30 21:30:00" and frame.time <= "2020-10-30 21:40:00"

# 特定の文字列でフィルタ
frame contains "test"
```
https://sugarsugar.conf.jp/wireshark%E3%81%AE%E3%83%95%E3%82%A3%E3%83%AB%E3%82%BF%E3%83%BC

時刻列を jst に変更

<img src="https://storage.googleapis.com/zenn-user-upload/aae0a8f875c7-20221231.jpg" width=250>
<img src="https://storage.googleapis.com/zenn-user-upload/a1ef95bcb9dd-20221231.png" width=250>

### pssh 

複数サーバに一括ログインをしてヒアドキュメントを実行

```bash
brew install pssh

# 使用例
pssh -h ~/Desktop/pssh/host.list -i -l ユーザー名 "ls -l /home" | grep  gc | wc -l
```

### mov -> gif 変換

```bash
brew install ffmpeg

# 変換
ffmpeg -i hogehoge.mov -r 24 fugafuga.gif

i ... インプットファイル
r .... フレームレート（秒間ファイル数）

# 確認
open -a /Applications/Google\ Chrome.app fugafuga.gif

# リサイズ（横幅1280でアスペクト比固定）
ffmpeg -i a.mov -vf scale=1280:-1 -r 12 a.gif
```

### ターミナルで json を扱う

```bash
brew install jq

# マニュアル
https://stedolan.github.io/jq/manual/
# 使用例
https://qiita.com/takeshinoda@github/items/2dec7a72930ec1f658af

# jsonサンプル
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

# -r は、出力結果からダブルクォートを除外
```

### fish shell

```bash
brew install fish

# fishを起動
fish

# fishを設定
fish_config
```

### gnu-sed

mac 標準の sed は BSD sed と言って微妙に使い物にならないので、 linux 標準の GNU sed をインストールしておく

```bash
brew install gnu-sed
```

### MySQL用CLI

```bash
brew update && brew install mycli
```

### 操作しているキーを画面に表示する

```bash
brew install keycastr --cask
```

### icnsファイルを作成

通常Macのアプリケーションバンドル(.app)の中には、そのアプリのアイコンとして「icns」ファイルが格納されている

```bash
$ brew install makeicns
$ makeicns -in icon.png -out icon.icns
```
https://softantenna.com/blog/makeicns/

### colima （DockerDesktop の代替）

```bash
brew install colima

# 起動
colima start
# オプションを付けて起動
colima start --cpu 1 --memory 2 --disk 10
# 停止
colima stop
```
https://github.com/abiosoft/colima

## すべてのアプリケーションの実行を許可

たまに入れられないアプリがあるので以下のコマンドで実行を許可する

```bash
sudo spctl --master-disable
```

## 大文字小文字を無視した TAB 補完を設定

```bash:.inputrc
# TAB補完時に大文字小文字を無視
set completion-ignore-case on

# ファイルタイプをカラフルにする
set colored-stats on

# TAB補完の接頭辞をカラフルにする
set colored-completion-prefix on

# 実行ファイルに印を付ける
set visible-stats on

# Bashをviモードにする
set editing-mode vi

# ↑↓キーでhisotoryから入力補完する（例えば、cat + ↑で過去のcat + XXX を呼び出す）
"\e[A":history-search-backward  # arrow up
"\e[B":history-search-forward  # arrow down
```

## スマート引用符をオフにする

<img src="https://storage.googleapis.com/zenn-user-upload/edf0bbbb6eae-20221231.jpg" width=250>

