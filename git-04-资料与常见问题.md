参考资料
=======


常见问题
-------

0. 什么情况下需要创建`branch`（分支）？

	Git默认会创建`master`分支，基本使用中，在这个分支上操作提交、获取代码即可。但通常再创建一个特定任务的分支，在此分支上（`check out`切换到此分支）操作是被推荐的。比如创建一个名为`develop`的分支，作为尚在开发中的功能开发，等到测试稳定后，再合并到`master`或其它分支上。
	
	常用我们应当使用在其它分支上开发，后 `merge` 到 `master` 分支的方式，以让`master`分支尽可能简洁。

0. 使用GUI操作加入缓存区（`stage changes`）时，为什么很慢？

	超多文件提交时，推荐使用命令操作（`git add *`），极为迅速。

0. 能否修改最近一次提交的说明文字或补充提交内容？

		git commit --amend
		
	此为修改最近一次的提交。即使已push到远程服务器也可使用。

0. 无法push到远程服务器，出现`Non-fast-forward`错误怎么解决？

	问题（Non-fast-forward）的出现原因在于：git仓库中已经有一部分代码，所以它不允许你直接把你的代码覆盖上去。于是你有2个选择方式：

	> 选择`Amend`提交时，之前已提交内容已push到远程服务器，会出现此错误

	1. 强推，即利用强覆盖方式用你本地的代码替代git仓库内的内容

			$ git push -f
			
		或
		
			$ git push origin master -f

	2. 先把git的东西fetch到你本地然后merge后再push

			$ git fetch
			$ git merge

0. 部分文件不希望被版本控制，怎么操作？

	工程根目录下添加 `.gitignore`文件，添加不希望被控制的文件或文件夹。

0. 误提交了文件怎么办？
	
	e.g. 删除误提交的`*.iml`文件，不会在本地文件系统中被删除
	
		git rm --cached *.iml

0. 怎么给文件重命名或删除？
	
	工程内的任何文件可随意修改、重命名、删除等，（不可随意改动工程根目录的`.git`文件夹及文件），在操作加入“缓存区“或“提交”（部分GUI可能将两步合并为一步，即为“提交”）时，Git会聪明的知道所有的改动。
	
	当然 Git 本身也提供了 `git mv` 等命令。
	
0. `fetch` 和 `pull` 有什么区别？

	- git fetch：相当于是从远程获取最新版本到本地，不会自动merge；
	- git pull：相当于是从远程获取最新版本并merge到本地；


0. 添加远程仓库的命令`git remote add origin <server>`中的 `origin` 是什么意思？

	远程服务器`<server>`的别名，可以是任意你喜欢的名字，默认为`origin`，就像默认分支名为`master`一样。
	

0. 怎么删除远程服务器上的分支？

	慎用
	
		git push --delete origin devel

0. 为什么报SSL错误？

	关闭命令：

		git config --global http.sslVerify false

0. 怎么设置非全局的用户名？

	git工程下执行：
	
		git config user.name yourname

0. 如何用命令行查看每个提交所在的分支及其分化衍合情况？

		git log --pretty=format:"%h %s" --graph
		git log --pretty=format:"%h - %an, %ar : %s" --graph

<img src="img/git-graph-demo.png" style="width:100%;" title="git graph demo">



0. windows下添加`git ssh`公钥

	- 安装git，从程序目录打开 “Git Bash”；
	- 在个人文件夹下（类似`C:\Documents and Settings\Administrator\`）键入命令：`ssh-keygen -t rsa -C "email@email.com"`，其中"email@email.com"是git账号；
	- 提醒你输入key的名称，直接回车；
	- 在个人文件夹下产生`.ssh`目录和两个文件：`id_rsa`和`id_rsa.pub`；
	- 用记事本打开`id_rsa.pub`文件，复制内容，即公钥，在git的网站上的ssh密钥管理页面，添加“公钥”内容，保存。

--------------------------------------------------------


参考资料
-------

0. **资源**

	- [Git安装](http://git-scm.com/book/zh/起步-安装-Git)
	- [Git简易指南](http://www.bootcss.com/p/git-guide/)
	- [Pro Git](http://git-scm.com/book/zh)
	- [apple xcode](https://developer.apple.com/downloads/index.action?name=Xcode)
	- [GitX(OS X git GUI)](http://rowanj.github.io/gitx/)
	- [msysgit(windows GUI)](http://msysgit.github.io/)
	- [SourceTree](http://www.sourcetreeapp.com/)
		支持Windows(Windows7及以上，OS X)

0. **免费的git服务**

	- [gitlab](https://gitlab.com/)(支持私有)
	- [github](https://github.com/)

