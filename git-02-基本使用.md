Git基本使用
==========


安装
---

- Mac OS X
- Windows
- Linux
- Solaris

[下载](http://git-scm.com/downloads) （下载对应版后，按说明安装）
> OS X需要已安装Command Line Tools，下载地址[https://developer.apple.com/downloads/index.action?name=Xcode](https://developer.apple.com/downloads/index.action?name=Xcode)


--------------------------------------------------------

使用
---

**创建新仓库**

创建新文件夹，打开，然后执行 
	
	git init
	
以创建新的 `git仓库`。

**检出仓库**

0. 执行如下命令以创建一个本地仓库的克隆版本：

		git clone /path/to/repository
	
0. 如果是远端服务器上的仓库，你的命令会是这个样子：

		git clone username@host:/path/to/repository
		
	> 项目目录下产生`.git`目录，它是 Git 用来保存元数据和对象数据库的地方。该目录非常重要，每次克隆镜像仓库的时候，实际拷贝的就是这个目录里面的数据。

**工作流**

你的本地仓库由 git 维护的三棵“树”组成。

- 第一个是你的 `工作目录`，它持有实际文件；
- 第二个是 `缓存区（Index）`，它像个缓存区域，临时保存你的改动；
- 最后是 `HEAD`，指向你最近一次提交后的结果。

<img src="img/trees.png" style="width:100%;" title="git tree">

**添加与提交**

0. 你可以计划改动（把它们添加到缓存区*add file into staged area*），使用如下命令：

		git add <filename>
		#或
		git add *
		
	> `git add`是个多功能命令，根据目标文件的状态不同，此命令的效果也不同：可以用它开始跟踪新文件，或者把已跟踪的文件放到暂存区，还能用于合并时把有冲突的文件标记为已解决状态等

0. 这是 git 基本工作流程的第一步；使用如下命令以实际提交改动：

		git commit -m "代码提交信息"

0. 现在，你的改动已经提交到了 HEAD，但是还没到你的远端仓库。


**推送改动**

0. 你的改动现在已经在本地仓库的 HEAD 中了。执行如下命令以将这些改动提交到远端仓库：

		git push origin master

	可以把 `master` 换成你想要推送的任何分支。 

0. 如果你还没有克隆现有仓库，并欲将你的仓库连接到某个远程服务器，你可以使用如下命令添加：

		git remote add origin <server>

	如此你就能够将你的改动推送到所添加的服务器上去了。


**分支**

分支是用来将特性开发绝缘开来的。在你创建仓库的时候，master 是“默认的”。在其他分支上进行开发，完成后再将它们合并到主分支上。
<img src="img/branches.png" style="width:100%"/>


0. 创建一个叫做`feature_x`的分支，并切换过去：

		git checkout -b feature_x

0. 切换回主分支：

		git checkout master

0. 再把新建的分支删掉：

		git branch -d feature_x

除非你*将分支推送到远端仓库*（以下命令），不然该分支就是不为他人所见的：

	git push origin <branch>


**更新与合并**

0. 要更新你的本地仓库至最新改动，执行 `git pull`，以在你的工作目录中 `获取（fetch）` 并 `合并（merge）` 远端的改动。

		git pull

0. 要合并其他分支到你的当前分支（例如 `master`），执行：

		git merge <branch>

两种情况下，git 都会尝试去自动合并改动。不幸的是，自动合并并非次次都能成功，并可能导致 `冲突（conflicts）`。 这时候就需要你修改这些文件来人肉合并这些 `冲突（conflicts）` 了。改完之后，你需要执行如下命令以将它们标记为合并成功：

	git add <filename>
	
在合并改动之前，也可以使用如下命令查看：

	git diff <source_branch> <target_branch>


**标签**

在软件发布时创建标签，是被推荐的。这是个旧有概念，在 `SVN` 中也有。可以执行如下命令以创建一个叫做 `1.0.0` 的标签：

	git tag v1.0.0 1b2e1d63ff
	
	#追加标签的附注
	git tag -a v1.0.0 -m 'my version 1.4'
	git show v1.0.0
	#查看所有标签
	git tag

`1b2e1d63ff` 是你想要标记的提交 `ID 的前 10 位字符`。使用如下命令获取提交 `ID`：
	
	git log
	
你也可以用该提交 `ID` 的少一些的前几位，只要它是唯一的。


**替换本地改动**

0. 假如你做错事（自然，这是不可能的），你可以使用如下命令替换掉本地改动：

		git checkout -- <filename>

	此命令会使用 `HEAD` 中的最新内容替换掉你的工作目录中的文件。已添加到缓存区的改动，以及新文件，都不受影响。

0. 假如你想要丢弃你所有的本地改动与提交，可以到服务器上获取最新的版本并将你本地主分支指向到它：

		git fetch origin
		git reset --hard origin/master


**删除误提交的文件**（不会删除文件）

	git rm --cached *.iml


------------------------------------------------------

**其它**

0. *忽略某些文件*，项目根目录添加`.gitignore`文件，添加需要忽略文件列表，e.g.

		此为注释 – 将被 Git 忽略
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
		
	
	文件 .gitignore 的格式规范如下：

		- 所有空行或者以注释符号 ＃ 开头的行都会被 Git 忽略。
		- 可以使用标准的 glob 模式（shell 所使用的简化了的正则表达式）匹配。
		- 匹配模式最后跟反斜杠（/）说明要忽略的是目录。
		- 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。
	
	> 要养成一开始就设置好 .gitignore 文件的习惯，以免将来误提交这类文件。
	

0. 查看配置信息（配置文件位置：`/etc/gitconfig`, `~/.gitconfig`）

		git config --list

0. 远程仓库的删除和重命名

	在新版 Git 中可以用 `git remote rename` 命令修改某个远程仓库在本地的简称，比如想把 `pb` 改成 `paul`，可以这么运行：

		$ git remote rename pb paul
		$ git remote
		origin
		paul
		
	注意，对远程仓库的重命名，也会使对应的分支名称发生变化，原来的 `pb/master` 分支现在成了 `paul/master`。

	碰到远端仓库服务器迁移，或者原来的克隆镜像不再使用，又或者某个参与者不再贡献代码，那么需要移除对应的远端仓库，可以运行 `git remote rm` 命令：

		$ git remote rm paul
		$ git remote
		origin
		
0. 查看远程仓库信息

	我们可以通过命令 git remote show [remote-name] 查看某个远程仓库的详细信息，比如要看所克隆的 origin 仓库，可以运行：

		git remote -v
		git remote show origin
		

0. 更多常用命令

	- git status
	- git diff 
	- git add
	- git mv `移动`
	- git rm `删除`
	- git log `所有的提交日志`
		- git log -p -2 `最近2次的提交日志`
		- git log --pretty=oneline
		- git log --pretty=format:"%h - %an, %ar : %s"
		- git log --pretty=oneline --graph
	- git commit --amend `修改最后一次提交`
	
			$ git commit -m 'initial commit'
			$ git add forgotten_file
			$ git commit --amend
		
		上面的三条命令最终只是产生一个提交，第二个提交命令修正了第一个的提交内容。
		
	- git remote rename pb paul `把远程仓库由 pb 重命名为 paul`
	- git remote rm paul	
	- git push --delete origin devel `删除远程分支`
	- 
	- git svn clone -A users.txt http://example.com/svn/app/appname appname
	- git svn fetch
	- git remote set-url origin git://new.url.here `Change the URI (URL) for a remote Git repository`

