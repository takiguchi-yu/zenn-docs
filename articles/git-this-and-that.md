---
title: "gitあれこれ"
emoji: "🌟"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["git"]
published: false
---

# ~/.gitconfig
```conf
[core]
	excludesfile = ~/.gitignore_global
	quotepath = false
	hooksPath = ~/githooks
[color]
	status = auto

[user]
	name = 名前
	email = メアド
[commit]
	template = ~/.stCommitMsg
[push]
	default = nothing
[alias]
	st = status
	br = branch
	co = checkout
	cm = commit
	fp = fetch --prune
	lo = log --oneline
	lg = log --pretty=format:'%C(red)%h %C(reset)(%cd) %C(green)%an %Creset%s %C(yellow)%d%Creset' --graph --date=relative --name-status
	la = log --pretty=format:'%Cgreen%h %Creset%cd %Cblue[%cn] %Creset%s%C(yellow)%d%C(reset)' --graph --date=relative --decorate --all
	df = "!git la | peco | awk '{print $2}' | xargs -I {} git diff {}^ {}"
[grep]
	lineNumber = true
[merge]
	ff = false
[pull]
	ff = only
```

# コマンドラインで新しいリポジトリを作成する
```bash
echo "# hogehoge" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:ユーザー名/リポジトリ名.git
git push -u origin main

git config --global user.name "名前"
git config --global user.email メアド
```

# コマンドラインから既存のリポジトリをプッシュ
```bash
git remote add origin git@github.com:ユーザー名/リポジトリ名.git
git branch -M main
git push -u origin main
```

# fork 元の変更を fork 先に取り込む方法
```bash
# とりま現在のリモートリポジトリを確認
$ git remote -v
## fork 元のリポジトリを「fork_master」という名前で追加
$ git remote add fork_source フォーク元gitリポジトリ
# 追加されたことを確認
$ git remote -v
origin
fork_master
# 複数リモートを管理
git remote rename origin origin-2
git remote -v
# 追加したリポジトリをフェッチ
git fetch fork_source
# ブランチの一覧を確認
git branch -a
# マージ
git merge --no-ff fork_source/develop
(--no-ffはコミットログを残しますの意味)
あとは push すればおｋ
```

# リモートリポジトリを削除
git remote rm [repository name]

# 強制的にローカルを上書き
git fetch fork_source
git reset --hard fork_source/develop

# リモートブランチとの差分を見る
git branch -a
git diff

# コミット履歴を見る
git log --oneline
git log --graph --oneline --decorate --all
git log --pretty=format:"%h %ad %s" --date=short --all

# 複数あるコミットログをまとめる
git rebase -i HEAD~<遡ってまとめるログを数で指定>
例）過去 3 つ分のコミットログをまとめる
git rebase -i HEAD~3
pick
pick --> f
pick --> f

## 差分があったファイル名のみ
git diff --name-only {from_branch} {to_branch}
git diff --name-only remotes/origin/master feature/fugafuga

# ある 1 ファイルの変更点を見る
git diff -- {対象のファイルパス}

# 特定のブランチとファイルの差分を見る
git diff ブランチ A..ブランチ B -- 対象のファイルパス
git diff remotes/origin/master..feature/hogehoge -- configure/Application/index.html

# リモートブランチを https から ssh に切り替える
git remote -v
git remote set-url origin git@github.com:ユーザー名/リポジトリ名.git

# master とマージ
git pull master
git merge master

# 特定ファイルのバージョンを元に戻す
git checkout コミット ID ファイルパス
git checkout 8214db3738db9c632fe69cac7d97e5a3d18e13ec configure/Application/index.html

# 直前のコミットメッセージ修正
git commit --amend -m "変更メッセージ"

# 変更を退避する
git stash save
git stash save "メッセージ"

# 退避した作業の一覧を見る
git stash list

# 退避した作業を戻す
git stash apply stash@{0}

# 退避した作業を削除する
git stash drop stash@{0}

# 何を退避したかを見る
git stash show stash@{0}

# 「マージしたらコンフリクトした。コンフリクトを解消しようといろいろ編集した。でもやっぱりやめよう。」
コンフリクト解消のためにコードをいろいろ編集したけどやっぱりマージやめよう、というときです。

git reset --hard HEAD

# マージしたけど特定のマージを戻したいとき
git revert -m 1 コミット ID
git revert -m 1 8214db3738db9c632fe69cac7d97e5a3d18e13ec
そこで、 -m オプションが必要になります。
-m は mainline の略で、2 つの履歴のどちらを mainline として残したいかを 1 か 2 で指定します。
1 がマージされた側のブランチ（今回でいうと abc ブランチ）、2 がマージした側のブランチ（今回でいうと master ブランチ）を指します。
今回のように merge コミットを revert したい場合は、1 を指定すれば OK です。

→ マージを revert する場合は「-m 1」を付けないといけない

# コミット履歴ごと打ち消したい場合

git reset --hard HEAD^^

ひとつの^・・・直前のコミットを打ち消す
ふたつの^・・・さらにその前のコミットを打ち消す

revertの場合、同じコミットを元に、戻せないため、再リリースをする場合はresetをした方が良い。
→ revertの場合、コミット履歴が保持されるため、マージリクエストをしたときにすでにマージ済みとなり、差分が検出されない

# reset
develop を reset して再び対応内容をマージ
```bash
# developブランチをバックアップ
git checkout develop
git checkout -b develop-bk
git push -u origin HEAD

# 打ち消したいcommitまでresetする
git checkout develop
git reset --hard HEAD^^
git push -uf origin HEAD
```

# コンフリクト解消
## 前の変更を優先(HEAD(Current Change)が優先) 上が優先
git checkout --ours ファイル名

## ローカルの変更を優先(Incoming Change)が優先 下が優先
git checkout --theirs ファイル名

# リモートブランチをチェックアウト
git branch -r
git checkout -b [ブランチ名] [リモートブランチ名]

# 現在の変更を破棄
git checkout [filepath]

# ローカルのブランチを削除
git branch --delete [ブランチ名]

# git コマンドのショートカットを設定
git config --global alias.st status
git config --global alias.br branch
git config --global alias.co checkout
git config --global alias.cm commit
## 以下は .gitconfig に直書きする(コマンドだとエラーになるので)
git config --global alias.fp fetch --prune
git config --global alias.lo log --oneline
git config --global alias.lg log --graph --oneline --decorate --all
git config --global alias.lp log --pretty=format:"%h %ad %s" --date=short --all
# git grep したときに行番号を表示する
git config --global grep.lineNumber true

# 直前のコミット取り消し
git reset --hard HEAD^
--hard 変更内容ごと取り消す
--soft 変更内容は保持してコミットログだけを取り消す

## リモートリポジトリの変更
```bash
git remote set-url origin git@github.com:ユーザー名/リポジトリ名.git
```

リモートブランチをローカルにチェックアウト
# 現在のブランチを確認
```bash
$ git branch -a
  develop
* feature/hoge
  master
  remotes/origin/HEAD -> origin/master
  remotes/origin/develop
  remotes/origin/master
```

# 名前を付けてブランチをチェックアウト
$ git checkout -b feature/fuga origin/develop

# マージしたらコンフリクトしたのでやっぱりマージをやめたいとき
git merge --abort

# マージしたらコンフリクトしたので色々解消しようと頑張ったけどやっぱりマージをやめたいとき
git reset --hard HEAD

# ローカルを強制的にリモートにしたいとき
git fetch --prune 
git reset --hard origin/master

# git add を取り消す

## 1回目の場合
すべてのファイル
git rm --cached -r .

ファイル指定
git rm --cached -r {ファイル名}

## 2回目以降の場合

すべてのファイル
git reset HEAD

ファイル指定
git reset HEAD {ファイル名}

# リモートブランチをローカルに反映
git pull origin <リモートブランチ名>
git merge --no-ff feature/hogehoge
## コミットログ残さない
git merge <ブランチ名>
## コミットログ残す
git merge --no-ff <ブランチ名>

# サブモジュールが空の場合
git submodule init
git submodule update

# branch 削除
## ローカルブランチの削除
### マージ済み場合
git branch -d <ブランチ名>
### 未マージの場合
git branch -D <ブランチ名>

## リモートブランチ の削除
git push --delete <remote> <branch>
git push --delete origin hotfix

# 追跡ファイルの変更をもとに戻す(Changes not staged for commit:)
# すべてをもとに戻す
git checkout .

# 管理外ファイルの変更をもとに戻す(Untracked files:)
git clean -f 
# ディレクトリをもとに戻す場合
git clean -df
# dry-run 的なことをする場合
git clean -n

# Git の各ブランチの最終更新日、ブランチ名、コミットしたユーザー名を最終更新日が古い順に一覧で表示する
git branch -a --sort=authordate --format="%(authordate:relative)%09%(refname)%09%(authorname)"

# --diff-filter を使って差分を見る

git diff --name-only --diff-filter=MACR origin/master

M...Modified
A...Added
C...Copied
R...Renamaed
D...Deleted

# ブランチ名を変更する

git branch -m 古いブランチ 新しいブランチ

# ファイルの変更を追いかける

ファイルが削除されていても追いかけることができるので知っているとたまに便利

git log -- ファイル名フルパス

## 1コミット分だけを知りたい場合
git log -n 1 -- ファイル名フルパス

# remote を pull しようとして fatal: refusing to merge unrelated histories が出たとき
git merge --allow-unrelated-histories origin/master

# pull したときに Not possible to fast-forward, aborting. が出たとき
git pull --rebase

# 何かしらの理由で複数ブランチを管理したいとき
## 例は public フォルダだけは gh-pages というブランチ名で管理
git worktree add -B gh-pages public origin/gh-pages

# コミットメッセージ修正
## 直前のメッセージを修正
git commit --amend -m "message"

# patch
git diff > hoge.php.patch
patch -p1 < hoge.php.patch

-p1 は1階層上から差分取り込みを実行する
-p0 とするとpatchを充てる対象のディレクトリで実行する場合に使う

# サブモジュールを持ってくる

git submodule update

## 初回はこちら
git submodule update --init --recursive

# サブモジュールのURLを変更する

vi .gitmodules の url を書き換える
この時点ではまだ .git/config は書き換わっていない
git submodule sync
この時点で .git/config が書き換わる
git submodule update

