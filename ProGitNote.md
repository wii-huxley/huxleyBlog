---
title: ProGit阅读笔记
date: 2016-06-29 21:55:43
tags: ["git"]
categories: ["其他"]
page_pv: true
page_pv_header: 本文总阅读量
page_pv_footer: 次
---
## 基本配置

### 用户信息

用户信息

	$ git config --global user.name "John Doe"
	$ git config --global user.email johndoe@example.com

文本编译器

	$ git config --global core.editor emacs

差异分析工具

	$ git config --global merge.tool vimdiff

查看配置信息

	$ git config --list
	有时候会看到重复的变量名，那就说明它们来自不同的配置文件（比如
	/etc/gitconfig 和 ~/.gitconfig），不过最终 Git 实际采用的是最后一个。

	也可以直接查阅某个环境变量的设定，只要把特定的名字跟在后面即可，像这样：
	$ git config user.name

## Git 基本用法

### 取得项目的Git仓库

在工作目录中初始化新仓库

	$ git init

从现有仓库克隆

	$ git clone git://github.com/schacon/grit.git
	$ git clone git://github.com/schacon/grit.git mygrit

> 唯一的差别就是，现在新建的目录成了 mygrit，其他的都和上边的一样。

### 记录每次更新到仓库

> ![Alt text](/images/img_2_1.png)

> 图 2-1. 文件的状态变化周期

检查当前文件状态

	$ git status

> * Untracked files：未跟踪
> * Changes not staged for commit：已跟踪，未暂存
> * Changes to be committed：已暂存

跟踪新文件

	$ git add README

暂存已修改文件

    $ git add benchmarks.rb

忽略某些文件

	$ cat .gitignore
    *.[oa]
    *~

> * 星号（*）匹配零个或多个任意字符
> * [abc] 匹配任何一个列在方括号中的字符（这个例子要么匹配一个 a，要么匹配一个 b，要么匹配一个 c）
> * 问号（?）只匹配一个任意字符
> * 如果在方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配（比如 [0-9] 表示匹配所有 0 到 9 的数字）。

    # 此为注释 – 将被 Git 忽略
    # 忽略所有 .a 结尾的文件
    *.a
    # 但 lib.a 除外
    !lib.a
    # 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
    /TODO
    # 忽略 build/ 目录下的所有文件
    build/
    # 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
    doc/*.txt
    # ignore all .txt files in the doc/ directory
    doc/**/*.txt

查看已暂存和未暂存的更新

	$ git diff

> 比较的是工作目录中当前文件和暂存区域快照之间的差异，也就是修改之后还没有暂存起来的变化内容。

	git diff --cached

> 比较已暂存的文件和上次提交时的快照之间的差异

	git diff --staged

	//Git 1.6.1 及更高版本还允许使用,效果是相同的，但更好记些。
	git diff --staged

提交更新

	$ git commit

> git会启动文本编译器，以便输入本次提交的说明，文本中包含最后一次运行git status的输出，也可以用 `-v` 将修改差异的每一行都包含进来，退出编译器，git会去掉注释行，将说明内容和本次更新提交到仓库

	$ git commit -m "Story 182: Fix benchmarks for speed"
	[master 463dc4f] Story 182: Fix benchmarks for speed
	 2 files changed, 3 insertions(+)
	 create mode 100644 README

> 也可用 `-m` 参数后跟提交的方式

> 提交后它会告诉你，当前提交的分支( `master` )，本次提交的完整SHA-1校验( `463dc4f` )，有多少文件修订过，多少行增删改过

跳过使用暂存区域

	$ git commit -a -m 'added new benchmarks'

> 给 `git commit` 加上 `-a` 选项，git就会自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 `git add` 步骤

移除文件

	$ rm grit.gemspec

> 从工作目录中手工删除文件，运行 `git status` 时就会在 `Changes not staged for commit` 部分看到

	$ git rm grit.gemspec

> 提交后，该文件就不再纳入版本管理了，如果删除之前修改过并且已经放到暂存区，则必须要用强制删除选项 `-f` ，以防误删文件后丢失修改的内容

	$ git rm --cached readme.txt

> 把文件从git仓库中删除，但仍保留在工作目录

移动文件

	$ git mv file_from file_to

> 修改文件名字

### 查看提交历史

	$ git log

> 按照提交时间列出所有的更新，每次更新都有一个 SHA-1 校验、name、email、提交时间和最后缩进一个段落显示提交说明

	$ git log -p -2

> `-p` 选项展开显示每次提交的内容差异，用 `-2` 则仅显示最近的两次更新

	$ git log -U1 --word-diff

> 这里的对比显示在行间，新增的单词被 `{+ +}` 括起来，被删除的单词被 `[- -]` 括起来，`-U1` 使上下文(context)行数从默认的 3 行，减为 1 行

	$ git log --stat

> 每个提交都列出了修改过的文件，以及其中添加和移除的行数，并在最后列出所有增减行数小计

	$ git log --pretty=oneline

> 将每个提交放在一行显示，这在提交数很大时非常有用。另外还有 `short`，`full` 和 `fuller` 可以用，展示的信息或多或少有些不同

	$ git log --pretty=format:"%h - %an, %ar : %s"

	选项	 说明
	%H	  提交对象（commit）的完整哈希字串
	%h	  提交对象的简短哈希字串
	%T	  树对象（tree）的完整哈希字串
	%t	  树对象的简短哈希字串
	%P	  父对象（parent）的完整哈希字串
	%p	  父对象的简短哈希字串
	%an	  作者（author）的名字
	%ae	  作者的电子邮件地址
	%ad	  作者修订日期（可以用 -date= 选项定制格式）
	%ar	  作者修订日期，按多久以前的方式显示
	%cn	  提交者(committer)的名字
	%ce	  提交者的电子邮件地址
	%cd	  提交日期
	%cr	  提交日期，按多久以前的方式显示
	%s	  提交说明

> 定制要显示的记录格式，这样的输出便于后期编程提取分析

	$ git log --pretty=format:"%h %s" --graph

> 用 oneline 或 format 时结合 `--graph` 选项，可以看到开头多出一些 ASCII 字符串表示的简单图形，形象地展示了每个提交所在的分支及其分化衍合情况。

> 其他常用的选项及其释义

    选项             说明
    -p	            按补丁格式显示每个更新之间的差异。
    --word-diff	    按 word diff 格式显示差异。
    --stat	        显示每次更新的文件修改统计信息。
    --shortstat	    只显示 --stat 中最后的行数修改添加移除统计。
    --name-only	    仅在提交信息后显示已修改的文件清单。
    --name-status	显示新增、修改、删除的文件清单。
    --abbrev-commit	仅显示 SHA-1 的前几个字符，而非所有的 40 个字符。
    --relative-date	使用较短的相对时间显示（比如，“2 weeks ago”）。
    --graph	        显示 ASCII 图形表示的分支合并历史。
    --pretty        使用其他格式显示历史提交信息。可用的选项包括 oneline，
	                short，full，fuller 和 format（后跟指定格式）。
    --oneline	    `--pretty=oneline --abbrev-commit` 的简化用法。

限制输出长度

	$ git log --since=2.weeks

> 列出所有最近两周内的提交，你可以给出各种时间格式，比如说具体的某一天（“2008-01-15”），或者是多久以前（“2 years 1 day 3 minutes ago”）。

> 还可以给出若干搜索条件，列出符合的提交。用 `--author` 选项显示指定作者的提交，用 `--grep` 选项搜索提交说明中的关键字。（请注意，如果要得到同时满足这两个选项搜索条件的提交，就必须用 `--all-match` 选项。否则，满足任意一个条件的提交都会被匹配出来）

> 另一个真正实用的 `git log` 选项是路径(path)，如果只关心某些文件或者目录的历史提交，可以在 `git log` 选项的最后指定它们的路径。因为是放在最后位置上的选项，所以用两个短划线（ `--` ）隔开之前的选项和后面限定的路径名。

	选项               说明
	-(n)              仅显示最近的 n 条提交
	--since, --after  仅显示指定时间之后的提交。
	--until, --before 仅显示指定时间之前的提交。
	--author          仅显示指定作者相关的提交。
	--committer       仅显示指定提交者相关的提交。

> 其他常用的类似选项。

	$ git log --pretty="%h - %s" --author=gitster
	--since="2008-10-01" \--before="2008-11-01"
	--no-merges -- t/

> 2008年10月1日到2008年11月1日期间，gitster提交但未合并的测试脚本，位于项目的t/目录下的文件

使用图形化工具查阅提交历史

> 新版的git安装后，就安装了gitk，在项目工作目录中输入 gitk 命令后，就会启动 `gitk` 界面。

### 撤消操作

修改最后一次提交

	$ git commit --amend

> 此命令将使用当前的暂存区域快照提交。如果刚才提交完没有作任何改动，直接运行此命令的话，相当于有机会重新编辑提交说明，但将要提交的文件快照和之前的一样。

> 启动文本编辑器后，会看到上次提交时的说明，编辑它确认没问题后保存退出，就会使用新的提交说明覆盖刚才失误的提交。

	$ git commit -m 'initial commit'
	$ git add forgotten_file
	$ git commit --amend

> 三条命令最终只是产生一个提交，第二个提交命令修正了第一个的提交内容。

取消已经暂存的文件

	$ git reset HEAD benchmarks.rb

取消对文件的修改

	$ git checkout -- benchmarks.rb

> 该文件已经恢复到修改前的版本，这条命令有些危险，所有对文件的修改都没有了。如果只是想回退版本，同时保留刚才的修改以便将来继续工作，可以用下章介绍的 stashing 和分支来处理，应该会更好些。

### 远程仓库的使用

查看当前的远程库

	$ git remote

> 查看当前配置的远程仓库

	$ git remote -v
    bakkdoor  git://github.com/bakkdoor/grit.git
    cho45     git://github.com/cho45/grit.git
    defunkt   git://github.com/defunkt/grit.git
    koke      git://github.com/koke/grit.git
    origin    git@github.com:mojombo/grit.git

> 加上 -v 选项，显示对应的克隆地址，如果有多个远程仓库，此命令将全部列出，上面列出的地址只有 origin 用的是 SSH URL 链接，所以也只有这个仓库我能推送数据上去

添加远程仓库

	$ git remote add pb git://github.com/paulboone/ticgit.git

> 添加一个新的远程仓库，指定一个名字


从远程仓库抓取数据

	$ git fetch pb

> 要抓取所有 Paul 有的，但本地仓库没有的信息，只是将远端的数据拉到本地仓库，并不自动合并到当前工作分支，只有当你确实准备好了，才能手工合并。

	git pull
> 自动抓取数据下来，然后将远端分支自动合并到本地仓库中当前分支。

推送数据到远程仓库：

	$ git push origin master

查看远程仓库信息

	$ git remote show origin

远程仓库的删除和重命名

	$ git remote rename pb paul

> 修改远程仓库在本地的简称

	$ git remote rm paul

> 移除对应的远端仓库

### 打标签

列显已有的标签

	$ git tag

> 显示的标签按字母顺序排列

	$ git tag -l 'v1.4.2.*'

> 列出符合条件的标签

新建标签
> 标签有两种：
>
> 轻量级的：
>
> > 像是个不会变化的分支，实际上它就是个指向特定提交对象的引用
>
> 含附注的：
>
> > 实际上是存储在仓库中的一个独立对象，它有自身的校验和信息，包含着标签的名字，电子邮件地址和日期，以及标签说明，标签本身也允许使用 GNU Privacy Guard (GPG) 来签署或验证。
>
> 一般我们都建议使用含附注型的标签，以便保留相关信息；当然，如果只是临时性加注标签，或者不需要旁注额外信息，用轻量级标签也没问题。

含附注的标签

	$ git tag -a v1.4 -m 'my version 1.4'

签署标签

	$ git tag -s v1.5 -m 'my signed 1.5 tag'

> 使用自己的私钥，用 GPG 来签署标签，把之前的 -a 改为 -s

轻量级标签

	$ git tag v1.4-lw

验证标签

	$ git tag -v v1.4.2.1

后期加注标签

	$ git tag -a v1.2 9fceb02

> 在打标签的时候跟上对应提交对象的校验和（或前几位字符）

分享标签

	$ git push origin v1.5

> 默认情况下，git push 并不会把标签传送到远端服务器上，只有通过显式命令才能分享标签到远端仓库。其命令格式如同推送分支，运行 `git push origin [tagname]`

	$ git push origin --tags

> 一次推送所有本地新增的标签上去

### 技巧和窍门 ###

自动补全

> 如果你用的是 Bash shell，可以试试看 Git 提供的自动补全脚本。下载 Git 的源代码，进入 `contrib/completion` 目录，会看到一个 `git-completion.bash` 文件。将此文件复制到你自己的用户主目录中（译注：按照下面的示例，还应改名加上点：`cp git-completion.bash ~/.git-completion.bash`），并把下面一行内容添加到你的 `.bashrc` 文件中：

	source ~/.git-completion.bash

> 也可以为系统上所有用户都设置默认使用此脚本。Mac 上将此脚本复制到 /opt/local/etc/bash_completion.d 目录中，Linux 上则复制到 /etc/bash_completion.d/ 目录中。这两处目录中的脚本，都会在 Bash 启动时自动加载。

> 如果在 Windows 上安装了 msysGit，默认使用的 Git Bash 就已经配好了这个自动补全脚本，可以直接使用。

> 在输入 Git 命令的时候可以敲两次跳格键（Tab），就会看到列出所有匹配的可用命令建议

> 键入 git co 然后连按两次 Tab 键，会看到两个相关的建议（命令） commit 和 config。继而输入 m<tab> 会自动完成 git commit 命令的输入。

Git 命令别名

	$ git config --global alias.co checkout
	$ git config --global alias.br branch
	$ git config --global alias.ci commit
	$ git config --global alias.st status

> 用 git config 为命令设置别名后，如果要输入 git commit 只需键入 git ci 即可

	$ git config --global alias.unstage 'reset HEAD --'

	$ git unstage fileA
	$ git reset HEAD fileA

> 取消暂存文件时的输入， 这样一来，下面的两条命令完全等同：

	$ git config --global alias.last 'log -1 HEAD'

> 设置 last 命令，然后要看最后一次的提交信息，就变得简单多了

	$ git config --global alias.visual '!gitk'

> 不过有时候我们希望运行某个外部命令，而非 Git 的子命令，这个好办，只需要在命令前加上 `!` 就行。如果你自己写了些处理 Git 仓库信息的脚本的话，就可以用这种技术包装起来。作为演示，我们可以设置用 `git visual` 启动 `gitk`

## Git分支 ##

### 何谓分支 ###

> 在 Git 中提交时，会保存一个提交（commit）对象，该对象包含一个指向暂存内容快照的指针，包含本次提交的作者等相关附属信息，包含零个或多个指向该提交对象的父对象指针：首次提交是没有直接祖先的，普通提交有一个祖先，由两个或多个分支合并产生的提交则有多个祖先。

![](/images/img_3_1.png)

> 单个提交对象在仓库中的数据结构

![](/images/img_3_2.png)

> 多个提交对象之间的链接关系

### 分支的新建与合并 ###

### 分支的管理 ###

### 利用分支进行开发的工作流程 ###

### 远程分支 ###

### 分支的衍合 ###

## 服务器上的Git ##

### 协议 ###

### 在服务器上部署 Git ###

### 生成 SSH 公钥 ###

### 架设服务器 ###

### 公共访问 ###

### GitWeb ###

### Gitosis ###

### Gitolite ###

### Git 守护进程 ###

### Git 托管服务 ###

## 分布式 Git ##

### 分布式工作流程 ###

### 为项目作贡献 ###

### 项目的管理 ###

## Git 工具 ##

### 修订版本（Revision）选择 ###

### 交互式暂存 ###

### 储藏（Stashing） ###

### 重写历史 ###

### 使用 Git 调试 ###

### 子模块 ###

### 子树合并 ###

## 自定义 Git ##

### 配置 Git ###

### Git属性 ###

### Git挂钩 ###

### Git 强制策略实例 # ###

## Git与其他系统 ##

### Git 与 Subversion ###

### 迁移到 Git ###

## Git 内部原理 ##

### 底层命令 (Plumbing) 和高层命令 (Porcelain) ###

### Git 对象 ###

### Git References ###

### Packfiles ###

### The Refspec ###

### 传输协议 ###

### 维护及数据恢复 ###
