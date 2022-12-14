---
title: "gitãããã"
emoji: "ð"
type: "idea" # tech: æè¡è¨äº / idea: ã¢ã¤ãã¢
topics: ["git"]
published: false
---

# ã³ãã³ãã©ã¤ã³ã§æ°ãããªãã¸ããªãä½æãã
```bash
echo "# hogehoge" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:ã¦ã¼ã¶ã¼å/ãªãã¸ããªå.git
git push -u origin main

git config --global user.name "åå"
git config --global user.email ã¡ã¢ã
```

# ã³ãã³ãã©ã¤ã³ããæ¢å­ã®ãªãã¸ããªãããã·ã¥
```bash
git remote add origin git@github.com:ã¦ã¼ã¶ã¼å/ãªãã¸ããªå.git
git branch -M main
git push -u origin main
```

# fork åã®å¤æ´ã fork åã«åãè¾¼ãæ¹æ³
```bash
# ã¨ãã¾ç¾å¨ã®ãªã¢ã¼ããªãã¸ããªãç¢ºèª
$ git remote -v
## fork åã®ãªãã¸ããªããfork_masterãã¨ããååã§è¿½å 
$ git remote add fork_source ãã©ã¼ã¯ågitãªãã¸ããª
# è¿½å ããããã¨ãç¢ºèª
$ git remote -v
origin
fork_master
# è¤æ°ãªã¢ã¼ããç®¡ç
git remote rename origin origin-2
git remote -v
# è¿½å ãããªãã¸ããªããã§ãã
git fetch fork_source
# ãã©ã³ãã®ä¸è¦§ãç¢ºèª
git branch -a
# ãã¼ã¸
git merge --no-ff fork_source/develop
(--no-ffã¯ã³ãããã­ã°ãæ®ãã¾ãã®æå³)
ãã¨ã¯ push ããã°ãï½
```

# ãªã¢ã¼ããªãã¸ããªãåé¤
git remote rm [repository name]

# å¼·å¶çã«ã­ã¼ã«ã«ãä¸æ¸ã
git fetch fork_source
git reset --hard fork_source/develop

# ãªã¢ã¼ããã©ã³ãã¨ã®å·®åãè¦ã
git branch -a
git diff

# ã³ãããå±¥æ­´ãè¦ã
git log --oneline
git log --graph --oneline --decorate --all
git log --pretty=format:"%h %ad %s" --date=short --all

# è¤æ°ããã³ãããã­ã°ãã¾ã¨ãã
git rebase -i HEAD~<é¡ã£ã¦ã¾ã¨ããã­ã°ãæ°ã§æå®>
ä¾ï¼éå» 3 ã¤åã®ã³ãããã­ã°ãã¾ã¨ãã
git rebase -i HEAD~3
pick
pick --> f
pick --> f

## å·®åããã£ããã¡ã¤ã«åã®ã¿
git diff --name-only {from_branch} {to_branch}
git diff --name-only remotes/origin/master feature/fugafuga

# ãã 1 ãã¡ã¤ã«ã®å¤æ´ç¹ãè¦ã
git diff -- {å¯¾è±¡ã®ãã¡ã¤ã«ãã¹}

# ç¹å®ã®ãã©ã³ãã¨ãã¡ã¤ã«ã®å·®åãè¦ã
git diff ãã©ã³ã A..ãã©ã³ã B -- å¯¾è±¡ã®ãã¡ã¤ã«ãã¹
git diff remotes/origin/master..feature/hogehoge -- configure/Application/index.html

# ãªã¢ã¼ããã©ã³ãã https ãã ssh ã«åãæ¿ãã
git remote -v
git remote set-url origin git@github.com:ã¦ã¼ã¶ã¼å/ãªãã¸ããªå.git

# master ã¨ãã¼ã¸
git pull master
git merge master

# ç¹å®ãã¡ã¤ã«ã®ãã¼ã¸ã§ã³ãåã«æ»ã
git checkout ã³ããã ID ãã¡ã¤ã«ãã¹
git checkout 8214db3738db9c632fe69cac7d97e5a3d18e13ec configure/Application/index.html

# ç´åã®ã³ãããã¡ãã»ã¼ã¸ä¿®æ­£
git commit --amend -m "å¤æ´ã¡ãã»ã¼ã¸"

# å¤æ´ãéé¿ãã
git stash save
git stash save "ã¡ãã»ã¼ã¸"

# éé¿ããä½æ¥­ã®ä¸è¦§ãè¦ã
git stash list

# éé¿ããä½æ¥­ãæ»ã
git stash apply stash@{0}

# éé¿ããä½æ¥­ãåé¤ãã
git stash drop stash@{0}

# ä½ãéé¿ããããè¦ã
git stash show stash@{0}

# ããã¼ã¸ãããã³ã³ããªã¯ããããã³ã³ããªã¯ããè§£æ¶ãããã¨ããããç·¨éãããã§ããã£ã±ããããããã
ã³ã³ããªã¯ãè§£æ¶ã®ããã«ã³ã¼ããããããç·¨éãããã©ãã£ã±ããã¼ã¸ãããããã¨ããã¨ãã§ãã

git reset --hard HEAD

# ãã¼ã¸ãããã©ç¹å®ã®ãã¼ã¸ãæ»ãããã¨ã
git revert -m 1 ã³ããã ID
git revert -m 1 8214db3738db9c632fe69cac7d97e5a3d18e13ec
ããã§ã -m ãªãã·ã§ã³ãå¿è¦ã«ãªãã¾ãã
-m ã¯ mainline ã®ç¥ã§ã2 ã¤ã®å±¥æ­´ã®ã©ã¡ãã mainline ã¨ãã¦æ®ããããã 1 ã 2 ã§æå®ãã¾ãã
1 ããã¼ã¸ãããå´ã®ãã©ã³ãï¼ä»åã§ããã¨ abc ãã©ã³ãï¼ã2 ããã¼ã¸ããå´ã®ãã©ã³ãï¼ä»åã§ããã¨ master ãã©ã³ãï¼ãæãã¾ãã
ä»åã®ããã« merge ã³ãããã revert ãããå ´åã¯ã1 ãæå®ããã° OK ã§ãã

â ãã¼ã¸ã revert ããå ´åã¯ã-m 1ããä»ããªãã¨ãããªã

# ã³ãããå±¥æ­´ãã¨æã¡æ¶ãããå ´å

git reset --hard HEAD^^

ã²ã¨ã¤ã®^ã»ã»ã»ç´åã®ã³ããããæã¡æ¶ã
ãµãã¤ã®^ã»ã»ã»ããã«ãã®åã®ã³ããããæã¡æ¶ã

revertã®å ´åãåãã³ããããåã«ãæ»ããªããããåãªãªã¼ã¹ãããå ´åã¯resetãããæ¹ãè¯ãã
â revertã®å ´åãã³ãããå±¥æ­´ãä¿æãããããããã¼ã¸ãªã¯ã¨ã¹ããããã¨ãã«ãã§ã«ãã¼ã¸æ¸ã¿ã¨ãªããå·®åãæ¤åºãããªã

# reset
develop ã reset ãã¦åã³å¯¾å¿åå®¹ããã¼ã¸
```bash
# developãã©ã³ããããã¯ã¢ãã
git checkout develop
git checkout -b develop-bk
git push -u origin HEAD

# æã¡æ¶ãããcommitã¾ã§resetãã
git checkout develop
git reset --hard HEAD^^
git push -uf origin HEAD
```

# ã³ã³ããªã¯ãè§£æ¶
## åã®å¤æ´ãåªå(HEAD(Current Change)ãåªå) ä¸ãåªå
git checkout --ours ãã¡ã¤ã«å

## ã­ã¼ã«ã«ã®å¤æ´ãåªå(Incoming Change)ãåªå ä¸ãåªå
git checkout --theirs ãã¡ã¤ã«å

# ãªã¢ã¼ããã©ã³ãããã§ãã¯ã¢ã¦ã
git branch -r
git checkout -b [ãã©ã³ãå] [ãªã¢ã¼ããã©ã³ãå]

# ç¾å¨ã®å¤æ´ãç ´æ£
git checkout [filepath]

# ã­ã¼ã«ã«ã®ãã©ã³ããåé¤
git branch --delete [ãã©ã³ãå]

# ããä½¿ãã³ãã³ãã®ã¨ã¤ãªã¢ã¹è¨­å®
git config --global alias.st status
git config --global alias.br branch
git config --global alias.co checkout
git config --global alias.cm commit
## ä»¥ä¸ã¯ .gitconfig ã«ç´æ¸ããã(ã³ãã³ãã ã¨ã¨ã©ã¼ã«ãªãã®ã§)
git config --global alias.fp fetch --prune
git config --global alias.lo log --oneline
git config --global alias.lg log --graph --oneline --decorate --all
git config --global alias.lp log --pretty=format:"%h %ad %s" --date=short --all
# git grep ããã¨ãã«è¡çªå·ãè¡¨ç¤ºãã
git config --global grep.lineNumber true

# ç´åã®ã³ãããåãæ¶ã
git reset --hard HEAD^
--hard å¤æ´åå®¹ãã¨åãæ¶ã
--soft å¤æ´åå®¹ã¯ä¿æãã¦ã³ãããã­ã°ã ããåãæ¶ã

## ãªã¢ã¼ããªãã¸ããªã®å¤æ´
```bash
git remote set-url origin git@github.com:ã¦ã¼ã¶ã¼å/ãªãã¸ããªå.git
```

ãªã¢ã¼ããã©ã³ããã­ã¼ã«ã«ã«ãã§ãã¯ã¢ã¦ã
# ç¾å¨ã®ãã©ã³ããç¢ºèª
```bash
$ git branch -a
  develop
* feature/hoge
  master
  remotes/origin/HEAD -> origin/master
  remotes/origin/develop
  remotes/origin/master
```

# ååãä»ãã¦ãã©ã³ãããã§ãã¯ã¢ã¦ã
$ git checkout -b feature/fuga origin/develop

# ãã¼ã¸ãããã³ã³ããªã¯ãããã®ã§ãã£ã±ããã¼ã¸ãããããã¨ã
git merge --abort

# ãã¼ã¸ãããã³ã³ããªã¯ãããã®ã§è²ãè§£æ¶ãããã¨é å¼µã£ããã©ãã£ã±ããã¼ã¸ãããããã¨ã
git reset --hard HEAD

# ã­ã¼ã«ã«ãå¼·å¶çã«ãªã¢ã¼ãã«ãããã¨ã
git fetch --prune 
git reset --hard origin/master

# git add ãåãæ¶ã

## 1åç®ã®å ´å
ãã¹ã¦ã®ãã¡ã¤ã«
git rm --cached -r .

ãã¡ã¤ã«æå®
git rm --cached -r {ãã¡ã¤ã«å}

## 2åç®ä»¥éã®å ´å

ãã¹ã¦ã®ãã¡ã¤ã«
git reset HEAD

ãã¡ã¤ã«æå®
git reset HEAD {ãã¡ã¤ã«å}

# ãªã¢ã¼ããã©ã³ããã­ã¼ã«ã«ã«åæ 
git pull origin <ãªã¢ã¼ããã©ã³ãå>
git merge --no-ff feature/hogehoge
## ã³ãããã­ã°æ®ããªã
git merge <ãã©ã³ãå>
## ã³ãããã­ã°æ®ã
git merge --no-ff <ãã©ã³ãå>

# ãµãã¢ã¸ã¥ã¼ã«ãç©ºã®å ´å
git submodule init
git submodule update

# branch åé¤
## ã­ã¼ã«ã«ãã©ã³ãã®åé¤
### ãã¼ã¸æ¸ã¿å ´å
git branch -d <ãã©ã³ãå>
### æªãã¼ã¸ã®å ´å
git branch -D <ãã©ã³ãå>

## ãªã¢ã¼ããã©ã³ã ã®åé¤
git push --delete <remote> <branch>
git push --delete origin hotfix

# è¿½è·¡ãã¡ã¤ã«ã®å¤æ´ããã¨ã«æ»ã(Changes not staged for commit:)
# ãã¹ã¦ããã¨ã«æ»ã
git checkout .

# ç®¡çå¤ãã¡ã¤ã«ã®å¤æ´ããã¨ã«æ»ã(Untracked files:)
git clean -f 
# ãã£ã¬ã¯ããªããã¨ã«æ»ãå ´å
git clean -df
# dry-run çãªãã¨ãããå ´å
git clean -n

# Git ã®åãã©ã³ãã®æçµæ´æ°æ¥ããã©ã³ãåãã³ãããããã¦ã¼ã¶ã¼åãæçµæ´æ°æ¥ãå¤ãé ã«ä¸è¦§ã§è¡¨ç¤ºãã
git branch -a --sort=authordate --format="%(authordate:relative)%09%(refname)%09%(authorname)"

# --diff-filter ãä½¿ã£ã¦å·®åãè¦ã

git diff --name-only --diff-filter=MACR origin/master

M...Modified
A...Added
C...Copied
R...Renamaed
D...Deleted

# ãã©ã³ãåãå¤æ´ãã

git branch -m å¤ããã©ã³ã æ°ãããã©ã³ã

# ãã¡ã¤ã«ã®å¤æ´ãè¿½ãããã

ãã¡ã¤ã«ãåé¤ããã¦ãã¦ãè¿½ãããããã¨ãã§ããã®ã§ç¥ã£ã¦ããã¨ãã¾ã«ä¾¿å©

git log -- ãã¡ã¤ã«åãã«ãã¹

## 1ã³ãããåã ããç¥ãããå ´å
git log -n 1 -- ãã¡ã¤ã«åãã«ãã¹

# remote ã pull ãããã¨ãã¦ fatal: refusing to merge unrelated histories ãåºãã¨ã
git merge --allow-unrelated-histories origin/master

# pull ããã¨ãã« Not possible to fast-forward, aborting. ãåºãã¨ã
git pull --rebase

# ä½ãããã®çç±ã§è¤æ°ãã©ã³ããç®¡çãããã¨ã
## ä¾ã¯ public ãã©ã«ãã ãã¯ gh-pages ã¨ãããã©ã³ãåã§ç®¡ç
git worktree add -B gh-pages public origin/gh-pages

# ã³ãããã¡ãã»ã¼ã¸ä¿®æ­£
## ç´åã®ã¡ãã»ã¼ã¸ãä¿®æ­£
git commit --amend -m "message"

# patch
git diff > hoge.php.patch
patch -p1 < hoge.php.patch

-p1 ã¯1éå±¤ä¸ããå·®ååãè¾¼ã¿ãå®è¡ãã
-p0 ã¨ããã¨patchãåã¦ãå¯¾è±¡ã®ãã£ã¬ã¯ããªã§å®è¡ããå ´åã«ä½¿ã

# ãµãã¢ã¸ã¥ã¼ã«ãæã£ã¦ãã

git submodule update

## ååã¯ãã¡ã
git submodule update --init --recursive

# ãµãã¢ã¸ã¥ã¼ã«ã®URLãå¤æ´ãã

vi .gitmodules ã® url ãæ¸ãæãã
ãã®æç¹ã§ã¯ã¾ã  .git/config ã¯æ¸ãæãã£ã¦ããªã
git submodule sync
ãã®æç¹ã§ .git/config ãæ¸ãæãã
git submodule update

## éçºã®æµã
```bash
# ã­ã¼ã«ã«ãã©ã³ããä½æ
git checkout -b <ä»»æã®ãã©ã³ãå>

# å¤æ´åå®¹ãç¢ºèª
git status

# æ´æ°åå®¹ãã¹ãã¼ã¸ã³ã°ã«ç»é²
git add .

# å·®åç¢ºèª
git diff --cached -w 

# ã­ã¼ã«ã«ãã©ã³ãã«ã³ããã
git commit -m"<ã¯ã³ã©ã¤ã³ã³ã¡ã³ã>"

# ã³ãããã­ã°ãç¢ºèª
git log
git reflog

# git log ãã­ã¬ã¤ã«è¦ãããã®ãããã
git log --graph --oneline --decorate --all
git log --pretty=format:"%h %ad %s" --date=short --all

# è¤æ°ããã³ãããã­ã°ãã¾ã¨ãã
git rebase -i HEAD~<é¡ã£ã¦ã¾ã¨ããã­ã°ãæ°ã§æå®>
# ä¾ï¼éå»3ã¤åã®ã³ãããã­ã°ãã¾ã¨ãã
# git rebase -i HEAD~3
# pick
# pick --> f
# pick --> f

# ãªã¢ã¼ããã©ã³ããæ´æ°
git push -u origin HEAD
```

## ç¾å¨ã®ãã©ã³ããç¢ºèª
```bash
git branch -a
```

## ã­ã¼ã«ã«ãªãã¸ããªããªã¢ã¼ããªãã¸ããªã« push ã§ããªãã¨ã
ä»¥ä¸ã®ãããªã¨ã©ã¼ãçºçããã¨ãã®å¯¾å¦æ³
```
error: failed to push some refs to 'https://github.com/xxxx/xxxxx.git'
```
ã³ãã³ã:
```bash
git merge --allow-unrelated-histories origin/master
```

## æ¥æ¬èªã®æå­åããè§£æ¶ãã
```
$ git status
On branch master
 
Initial commit
 
Untracked files:
  (use "git add <file>..." to include in what will be committed)
 
  "\343\202\212\343\203\274\343\201\251\343\201\277\343\203\274.md"
 
nothing added to commit but untracked files present (use "git add" to track)
```
```bash
# èªåã ãã«é©ç¨
git config --local core.quotepath false

# å¨ä½ã«é©ç¨
git config --global core.quotepath false
```

## æ¢å­ã®gitãªãã¸ããªã«ã­ã¼ã«ã«ãpushãã
```bash
git remote add origin <git url>
git push -u origin master
```
## git reflog è©³ç´°
https://gist.github.com/kymmt90/9c997726b638b316f9be07aa4e3eea5e

## ã­ã¼ã«ã«ã®å¤æ´ãç ´æ£ãã
```bash
# ãã¡ã¤ã«åæå®
git checkout <filename>

# ç¹å®ã®ãã¡ã¤ã«ã§ã¯ãªããå¨ã¦ããã¨ã«æ»ã
git checkout .
```

## ãªã¢ã¼ããã©ã³ããã­ã¼ã«ã«ã«ãã§ãã¯ã¢ã¦ã
```bash
# ç¾å¨ã®ãã©ã³ããç¢ºèª
$ git branch -a
  develop
* feature/hoge
  master
  remotes/origin/HEAD -> origin/master
  remotes/origin/develop
  remotes/origin/master

# ååãä»ãã¦ãã©ã³ãããã§ãã¯ã¢ã¦ã
$ git checkout -b feature/fuga origin/develop
```

## ãªã¢ã¼ããªãã¸ããªãè¿½å 
```bash
git remote add origin git@github.com:ã¦ã¼ã¶ã¼å/ãªãã¸ããªå.git
```

## ãªã¢ã¼ããªãã¸ããªã®å¤æ´
```bash
git remote set-url origin git@github.com:ã¦ã¼ã¶ã¼å/ãªãã¸ããªå.git
```

## ç¹å®ãã£ã¬ã¯ããªã®ã³ãããå±¥æ­´ãåç§
```bash
git log -- <path>

# ä¾
git log -- . # ã«ã¬ã³ããã£ã¬ã¯ããª
git log -- css # css ãã£ã¬ã¯ããª
git log -- css js # css ã¨ js ãã£ã¬ã¯ããª
```
