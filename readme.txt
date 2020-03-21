一：基本操作
	1. 通过命令 git init 把这个目录变成git可以管理的仓库
	2.使用命令 git add 文件 添加到暂存区里面去
	3.用命令 git commit告诉Git，把文件提交到仓库
			git commit -m “提交的注释”
	4.通过命令git status来查看是否还有文件未提交
	5.底改了什么内容，如何查看呢？可以使用如下命令：git diff 文件 
	6.想查看下历史记录，如何查呢？我们现在可以使用命令 git log 演示
	7.文件到底改了什么内容，如何查看呢？git diff readme.txt 
	8.做了什么修改后，我们可以放心的提交到仓库了，提交修改和提交文件是一样的2步(第一步是git add 第二步是：git commit)。
二：版本回退：
	1.git log –pretty=oneline 查看历史提交记录
	2.回退第一种是：git reset --hard HEAD^ 
		那么如果要回退到上上个版本只需把HEAD^ 改成 HEAD^^ 以此类推
		退到前100个版本的话，git reset --hard HEAD~100 即可
	3.查看下 文件内容如下：通过命令cat readme.txt查看
	4.通过如下命令即可获取到版本号：git reflog 
	5.git checkout -- file 可以丢弃工作区的修改
	6.可以直接在文件目录中把文件删了，或者使用如上rm命令：rm b.txt，
		想彻底从版本库中删掉了此文件的话，可以再执行commit命令 提交掉
	7.没有commit之前，如果我想在版本库中恢复此文件如何操作呢？
三：远程仓库
	由于你的本地Git仓库和github仓库之间的传输是通过SSH加密的，所以需要一点设置：
	第一步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，
	如果有的话，直接跳过此如下命令，如果没有的话，打开命令行，输入如下命令：
	ssh-keygen -t rsa –C “youremail@example.com”, 
	id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人
四：如何添加远程库？
	我们已经在本地创建了一个Git仓库后，又想在github创建一个Git仓库，并且希望这两个仓库进行远程同步，
	这样github的仓库可以作为备份，又可以其他人通过该仓库来协作
	
	登录github上，然后在右上角找到“create a new repo”创建一个新的仓库
	
	在本地的testgit仓库下运行命令：
	git remote add origin https://github.com/tugenhua0707/testgit.git
	
	把本地库的内容推送到远程，使用 git push命令，
	实际上是把当前分支master推送到远程
	
	从现在起，只要本地作了提交，就可以通过如下命令：
	git push origin master
五：如何从远程库克隆？
	使用命令git clone克隆一个本地库了
六：创建与合并分支
	创建dev分支，然后切换到dev分支上。如下操作
	git checkout 命令加上 –b参数表示创建并切换，相当于如下2条命令
	git branch dev
	git checkout dev
	git branch查看分支，会列出所有的分支，当前分支前面会添加一个星号
	切换分支git checkout master
	合并到主分支，在master分支上，使用如下命令 git merge dev 如下所示
	
	总结创建与合并分支命令如下：
	查看分支：git branch
	创建分支：git branch name
	切换分支：git checkout name
	创建+切换分支：git checkout –b name
	合并某分支到当前分支：git merge name
	删除分支：git branch –d name
	
七：解决冲突
	Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容，其中<<<HEAD是指主分支修改的内容，
	>>>>>fenzhi1 是指fenzhi1上修改的内容，我们可以修改下如下后保存
	试图推送的有冲突，解决的办法也很简单，上面已经提示我们，
	先用git pull把最新的提交从origin/dev抓下来，然后在本地合并，解决冲突，
	再推送。
	
	原因是没有指定本地dev分支与远程origin/dev分支的链接，
	根据提示，设置dev和origin/dev的链接：
	如下：git branch --set-upstream dev origin/dev
	
八：多人协作。
	当你从远程库克隆时候，实际上Git自动把本地的master分支和远程的master分支对应起来了，并且远程库的默认名称是origin。
	
要查看远程库的信息 使用 git remote
要查看远程库的详细信息 使用 git remote –v

九：推送分支：
	推送分支就是把该分支上所有本地提交到远程库中，推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上：
	使用命令 git push origin master
十： 命令
	一、新建代码库

		# 在当前目录新建一个Git代码库
		$ git init
		 
		# 新建一个目录，将其初始化为Git代码库
		$ git init [project-name]
		 
		# 下载一个项目和它的整个代码历史
		$ git clone [url]
	二、配置

		# 显示当前的Git配置
		$ git config --list
		 
		# 编辑Git配置文件
		$ git config -e [--global]
		 
		# 设置提交代码时的用户信息
		$ git config [--global] user.name "[name]"
		$ git config [--global] user.email "[email address]"
	三、增加/删除文件

		# 添加指定文件到暂存区
		$ git add [file1] [file2] ...
		 
		# 添加指定目录到暂存区，包括子目录
		$ git add [dir]
		 
		# 添加当前目录的所有文件到暂存区
		$ git add .
		 
		# 添加每个变化前，都会要求确认
		# 对于同一个文件的多处变化，可以实现分次提交
		$ git add -p
		 
		# 删除工作区文件，并且将这次删除放入暂存区
		$ git rm [file1] [file2] ...
		 
		# 停止追踪指定文件，但该文件会保留在工作区
		$ git rm --cached [file]
		 
		# 改名文件，并且将这个改名放入暂存区
		$ git mv [file-original] [file-renamed]
	四、代码提交

		# 提交暂存区到仓库区
		$ git commit -m [message]
		 
		# 提交暂存区的指定文件到仓库区
		$ git commit [file1] [file2] ... -m [message]
		 
		# 提交工作区自上次commit之后的变化，直接到仓库区
		$ git commit -a
		 
		# 提交时显示所有diff信息
		$ git commit -v
		 
		# 使用一次新的commit，替代上一次提交
		# 如果代码没有任何新变化，则用来改写上一次commit的提交信息
		$ git commit --amend -m [message]
		 
		# 重做上一次commit，并包括指定文件的新变化
		$ git commit --amend [file1] [file2] ...
	五、分支

		# 列出所有本地分支
		$ git branch
		 
		# 列出所有远程分支
		$ git branch -r
		 
		# 列出所有本地分支和远程分支
		$ git branch -a
		 
		# 新建一个分支，但依然停留在当前分支
		$ git branch [branch-name]
		 
		# 新建一个分支，并切换到该分支
		$ git checkout -b [branch]
		 
		# 新建一个分支，指向指定commit
		$ git branch [branch] [commit]
		 
		# 新建一个分支，与指定的远程分支建立追踪关系
		$ git branch --track [branch] [remote-branch]
		 
		# 切换到指定分支，并更新工作区
		$ git checkout [branch-name]
		 
		# 切换到上一个分支
		$ git checkout -
		 
		# 建立追踪关系，在现有分支与指定的远程分支之间
		$ git branch --set-upstream [branch] [remote-branch]
		 
		# 合并指定分支到当前分支
		$ git merge [branch]
		 
		# 选择一个commit，合并进当前分支
		$ git cherry-pick [commit]
		 
		# 删除分支
		$ git branch -d [branch-name]
		 
		# 删除远程分支
		$ git push origin --delete [branch-name]
		$ git branch -dr [remote/branch]
	六、标签

		# 列出所有tag
		$ git tag
		 
		# 新建一个tag在当前commit
		$ git tag [tag]
		 
		# 新建一个tag在指定commit
		$ git tag [tag] [commit]
		 
		# 删除本地tag
		$ git tag -d [tag]
		 
		# 删除远程tag
		$ git push origin :refs/tags/[tagName]
		 
		# 查看tag信息
		$ git show [tag]
		 
		# 提交指定tag
		$ git push [remote] [tag]
		 
		# 提交所有tag
		$ git push [remote] --tags
		 
		# 新建一个分支，指向某个tag
		$ git checkout -b [branch] [tag]
	七、查看信息

		# 显示有变更的文件
		$ git status
		 
		# 显示当前分支的版本历史
		$ git log
		 
		# 显示commit历史，以及每次commit发生变更的文件
		$ git log --stat
		 
		# 搜索提交历史，根据关键词
		$ git log -S [keyword]
		 
		# 显示某个commit之后的所有变动，每个commit占据一行
		$ git log [tag] HEAD --pretty=format:%s
		 
		# 显示某个commit之后的所有变动，其"提交说明"必须符合搜索条件
		$ git log [tag] HEAD --grep feature
		 
		# 显示某个文件的版本历史，包括文件改名
		$ git log --follow [file]
		$ git whatchanged [file]
		 
		# 显示指定文件相关的每一次diff
		$ git log -p [file]
		 
		# 显示过去5次提交
		$ git log -5 --pretty --oneline
		 
		# 显示所有提交过的用户，按提交次数排序
		$ git shortlog -sn
		 
		# 显示指定文件是什么人在什么时间修改过
		$ git blame [file]
		 
		# 显示暂存区和工作区的差异
		$ git diff
		 
		# 显示暂存区和上一个commit的差异
		$ git diff --cached [file]
		 
		# 显示工作区与当前分支最新commit之间的差异
		$ git diff HEAD
		 
		# 显示两次提交之间的差异
		$ git diff [first-branch]...[second-branch]
		 
		# 显示今天你写了多少行代码
		$ git diff --shortstat "@{0 day ago}"
		 
		# 显示某次提交的元数据和内容变化
		$ git show [commit]
		 
		# 显示某次提交发生变化的文件
		$ git show --name-only [commit]
		 
		# 显示某次提交时，某个文件的内容
		$ git show [commit]:[filename]
		 
		# 显示当前分支的最近几次提交
		$ git reflog
	八、远程同步

		# 下载远程仓库的所有变动
		$ git fetch [remote]
		 
		# 显示所有远程仓库
		$ git remote -v
		 
		# 显示某个远程仓库的信息
		$ git remote show [remote]
		 
		# 增加一个新的远程仓库，并命名
		$ git remote add [shortname] [url]
		 
		# 取回远程仓库的变化，并与本地分支合并
		$ git pull [remote] [branch]
		 
		# 上传本地指定分支到远程仓库
		$ git push [remote] [branch]
		 
		# 强行推送当前分支到远程仓库，即使有冲突
		$ git push [remote] --force
		 
		# 推送所有分支到远程仓库
		$ git push [remote] --all
	九、撤销

		# 恢复暂存区的指定文件到工作区
		$ git checkout [file]
		 
		# 恢复某个commit的指定文件到暂存区和工作区
		$ git checkout [commit] [file]
		 
		# 恢复暂存区的所有文件到工作区
		$ git checkout .
		 
		# 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
		$ git reset [file]
		 
		# 重置暂存区与工作区，与上一次commit保持一致
		$ git reset --hard
		 
		# 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
		$ git reset [commit]
		 
		# 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
		$ git reset --hard [commit]
		 
		# 重置当前HEAD为指定commit，但保持暂存区和工作区不变
		$ git reset --keep [commit]
		 
		# 新建一个commit，用来撤销指定commit
		# 后者的所有变化都将被前者抵消，并且应用到当前分支
		$ git revert [commit]
		 
		# 暂时将未提交的变化移除，稍后再移入
		$ git stash
		$ git stash pop
	





