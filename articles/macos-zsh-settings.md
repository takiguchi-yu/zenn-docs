---
title: "Mac zsh settings"
emoji: "😽"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["mac"]
published: false
---

# ~/.zshenv
```bash
if [ -f /Applications/MacVim.app/Contents/MacOS/Vim ]; then
  alias vi='env LANG=ja_JP.UTF-8 /Applications/MacVim.app/Contents/MacOS/Vim "$@"'
  alias vim='env LANG=ja_JP.UTF-8 /Applications/MacVim.app/Contents/MacOS/Vim "$@"'
fi

alias ll='ls -lG'

export PATH=/Users/yudai/.nodebrew/current/bin:/Users/yudai/.nvm/versions/node/v5.12.0/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin

export NODE_ENV=dev
```
# ~/.zshrc
```bash
# ~/.zshrc は Zsh のインタラクティブシェル（ユーザーがコマンドを入力する画面）が起動した際に読み込まれる設定ファイルです。 
# Zsh スクリプトを実行したり、 zsh -c 'command...' でコマンドを実行したりしたときには読み込まれません。
# このファイルには主に Zsh の操作に関する設定を記述します。

# Emacs ライクな操作を有効にする（文字入力中に Ctrl-F,B でカーソル移動など）
# Vi ライクな操作が好みであれば `bindkey -v` とする
bindkey -e

# 自動補完を有効にする
# コマンドの引数やパス名を途中まで入力して <Tab> を押すといい感じに補完してくれる
# 例： `cd path/to/<Tab>`, `ls -<Tab>`
autoload -U compinit; compinit

# 入力したコマンドが存在せず、かつディレクトリ名と一致するなら、ディレクトリに cd する
# 例： /usr/bin と入力すると /usr/bin ディレクトリに移動
setopt auto_cd

# ↑を設定すると、 .. とだけ入力したら1つ上のディレクトリに移動できるので……
# 2つ上、3つ上にも移動できるようにする
alias ...='cd ../..'
alias ....='cd ../../..'

# "~hoge" が特定のパス名に展開されるようにする（ブックマークのようなもの）
# 例： cd ~hoge と入力すると /long/path/to/hogehoge ディレクトリに移動
#hash -d hoge=/long/path/to/hogehoge

# cd した先のディレクトリをディレクトリスタックに追加する
# ディレクトリスタックとは今までに行ったディレクトリの履歴のこと
# `cd +<Tab>` でディレクトリの履歴が表示され、そこに移動できる
setopt auto_pushd

# pushd したとき、ディレクトリがすでにスタックに含まれていればスタックに追加しない
setopt pushd_ignore_dups

# 拡張 glob を有効にする
# glob とはパス名にマッチするワイルドカードパターンのこと
# （たとえば `mv hoge.* ~/dir` における "*"）
# 拡張 glob を有効にすると # ~ ^ もパターンとして扱われる
# どういう意味を持つかは `man zshexpn` の FILENAME GENERATION を参照
setopt extended_glob

# 入力したコマンドがすでにコマンド履歴に含まれる場合、履歴から古いほうのコマンドを削除する
# コマンド履歴とは今まで入力したコマンドの一覧のことで、上下キーでたどれる
setopt hist_ignore_all_dups

# コマンドがスペースで始まる場合、コマンド履歴に追加しない
# 例： <Space>echo hello と入力
setopt hist_ignore_space

# <Tab> でパス名の補完候補を表示したあと、
# 続けて <Tab> を押すと候補からパス名を選択できるようになる
# 候補を選ぶには <Tab> か Ctrl-N,B,F,P
zstyle ':completion:*:default' menu select=1

# 単語の一部として扱われる文字のセットを指定する
# ここではデフォルトのセットから / を抜いたものとする
# こうすると、 Ctrl-W でカーソル前の1単語を削除したとき、 / までで削除が止まる
WORDCHARS='*?_-.[]~=&;!#$%^(){}<>'


# プロンプトの設定
if [ $UID -eq 0 ]; then
	# rootユーザーの場合
	PROMPT="%F{red}%n:%f%F{green}%d%f [%m] %% "
else
	# rootユーザー以外の場合
	PROMPT="%F{cyan}%n:%f%F{green}%d%f %% "
fi

# gitブランチ名を色付きで表示させるメソッド
function rprompt-git-current-branch {
	if [ ! -e ".git" ]; then
		# gitで管理されていないディレクトリは何も返却しない
		return
	fi

	local branch_name st branch_status
	
	branch_name=`git rev-parse --abbrev-ref HEAD 2> /dev/null`
	st=`git status 2> /dev/null`
	if [[ -n `echo "$st" | grep "^nothing to"` ]]; then
		# 全てのcommitされていクリーンな状態
		branch_status="%F{green}"
	elif [[ -n `echo "$st" | grep "^Untracked files"` ]]; then
		# gitに管理されていないファイルがある状態
		branch_status="%F{red}?"
	elif [[ -n `echo "$st" | grep "^Changes not staged for commit"` ]]; then
		# git add されていないファイルがある状態
		branch_status="%F{red}+"
	elif [[ -n `echo "$st" | grep "^Changes to be committed"` ]]; then
		# git commit されていないファイルがある状態
		branch_status="%F{yellow}!"
	elif [[ -n `echo "$st" | grep "^rebase in progress"` ]]; then
		# コンフリクトが起こった状態
		echo "%F{red}!(no branch)"
		return
	else 
		# 上記以外の状態の場合は青色で表示させる
		branch_status="%F{blue}"
	fi
	# ブランチ名を色付きで表示する
	echo "${branch_status}[$branch_name]"
}
# プロンプトが表示されるたびにプロンプト文字列を評価、置換する
setopt prompt_subst

# プロンプトの右側(RPROMPT)にメソッドの結果を表示させる
RPROMPT='`rprompt-git-current-branch`'
```