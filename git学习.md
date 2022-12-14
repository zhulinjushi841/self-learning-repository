##### 1.分支与合并 <br>
##### 1.1 分支<br>
分支在本地完成，速度快，要创建一个新的分支，需要使用branch命令。<br>

    git branch test

branch命令不会将我们带入分支，只是创建一个新分支。所以需要使用*checkout* 命令来更改分支。<br>

    git checkout test

第一个分支或主分支，被称为"master"。
对其他分支的更改不会反应在主分支上。如果想将更改提交到主分支，则需要切换回master分支，然后使用合并。<br>

    git checkout master
    git merge test

如果想要删除分支，使用-d标识。

    git branch -d test

在创建仓库的时候，master是默认的分支。在其他分支上进行开发，完成后再将
它们合并到当前分支上。
创建一个叫 feature的分支并切换过去：

    git checkout -b feature

切换回master主分支：

    git checkout master

除非将该分支推送到远端仓库，否则该分支就是不为他人所见的：

    git push origin <branch>

##### 1.2 更新与合并
要更新本地仓库至最新改动，执行：

    git pull

以在工作目录中获取(fetch)并 合并(merge)远端的改动。
要合并其他分支至当前的分支(例如master)，执行：

    git merge <branch>


##### 2.git工作区、暂存区和版本库
工作区：就是在电脑里能看到的实际目录。
暂存区：英文叫stage或者index。一般存放在.git目录下的index文件(.git/index)中，所以
把暂存区有时候也叫做索引(index)。
版本库：工作区有一个隐藏目录.git,这个不算是工作区，而是Git的版本库。

当对工作区修改(或新增)的文件执行git add命令时，暂存区的目录树被更新，同时工作区修改
(或新增)的文件内容被写入到对象库中的一个新的对象中，而该对象的ID被记录在暂存区的文件索引中。

当执行提交操作(git commit)时，暂存区的目录树写到版本库(对象库)中，master分支会做相应的
更新。即master指向的目录树就是提交暂存区的目录树。

当执行git rm --cached <file>命令时，会从暂存区删除文件，工作区则不会作出改变。



##### 3.git基本操作
Git的工作就是创建和保存项目的快照以及与之后的快照进行对比。
Git的常用命令包括：
git clone、git push、git add、git commit、git checkout、git pull

创建仓库命令
git init	初始化仓库
git clone	拷贝一份远程仓库，也就是下载一个项目

提交与修改
Git的工作就是创建和保存项目的快照与之后的快照进行对比。
命令		说明
git add 	添加文件到暂存区
git status	查看仓库当前的状态，显示有变更的文件
git diff	比较文件的不同，即暂存区和工作区的差异
git rm		将文件从暂存区和工作区中删除
git mv	移动或者重命名工作区文件
git commit	提交暂存区到本地仓库
git reset	回退版本

提交日志
命令		说明
git log	查看历史提交记录
git blame <file> 以列表形式查看指定文件的历史修改记录

远程操作
命令		说明
git remote	远程仓库操作
git fetch	从远程获取代码库
git pull	下载远程代码并合并
git push	上传远程代码并合并



##### 3.1 git reset命令
git reset命令用于回退版本，可以指定退回某一次提交的版本
git reset命令语法格式如下：
git reset [--soft/--mixed/--hard] [HEAD]

    git reset HEAD 

后面什么都不跟的，就是上一次add 里面的内容全部撤销。

    git reset HEAD XXX 

后面跟文件名，就是对某个文件进行撤销。

--mixed为默认，可以不用带该参数，用于重置暂存区的文件与上一次的提交(commit)保持一致。
不删除工作区改动代码，撤销commit，并撤销git
 add .，操作这个为默认参数，也就是说：
 使用git reset --mixed HEAD^ 和 git reset HEAD^的效果是一样的。
git reset [HEAD]
实例：
git reset HEAD^	#回退到所有内容到上一个版本

--soft参数用于回退到某个版本：
git reset --soft HEAD~3	#回退到上上上一个版本
--soft 不删除工作区改动代码，撤销commit，不撤销git add . 

--hard参数撤销工作区中所有未提交的修改内容，将暂存区与工作区都回退到之前的所有信息提交：
git reset --hard bae123	#回退到某个版本回退点之前的所有信息
git reset --hard origin/master	#将本地的状态回退到和远程的保持一致
--hard 删除工作区改动代码，撤销commit，撤销git add .
完成这项操作后，就恢复到了指定版本commit时的状态。
如果commit的注释写错了，只是想改一下注释，只需要：

    git commit --amend 

此时会进入到默认vim编辑器中，修改注释完毕后保存即可。

##### 3.2 Git创建仓库
Git使用git init命令来初始化一个Git仓库，Git许多命令需要在Git的仓库中运行，
所以git init是使用Git的第一个命令。
在执行完git init命令后，Git仓库会生成一个.git目录，该目录包含了资源的所有元数据，其他的
项目目录保持不变。

##### 3.3 git clone
我们使用git clone从现有的Git仓库中拷贝项目
克隆仓库的命令格式为：
git clone <repo>
git clone <repo> <directory>
参数说明：
repo：Git仓库
directory：本地目录
在Github上，一个项目实际上只有一个clone链接
因此，如果想要从某个特定分支上clone代码：
git clone -b 分支名字 xxx（链接）

##### 3.4 git config配置
git的设置使用git config命令。
显示当前的git配置信息：
git config --list
设置提交代码时的用户信息：
git config --global user.name "jerome"
git config --global user.email test@qq.com
如果去掉--global参数则只对当前仓库有效。

##### 3.5 git fetch
git fetch命令从远端仓库中下载commits,files,refs到本地仓库中。
当需要查看其他人的工作的时候，就需要使用fetch命令。
这个操作会让用户看到远端仓库的所有提交进展，但是fetch命令并不会强迫远端的变更合并到仓库中。
Git会对本地内容与fetch下载的内容进行隔离，这就保证了fetch命令更新的远端变更不会对本地正在进行的开发工作产生任何影响。
如果想查看fetch命令下载的内容，需要显式地通过 git checkout 命令检出希望查看的版本。

因此，在不想让远端仓库的版本合并到本地之前，但仍然希望可以查看一下远端版本都做了哪些变更的时候，fetch命令就是一种安全的解决方案。
可以使用 git diff 命令查看fetch下载内容与当前工作区的变更区别。

##### 3.6 创建.gitignore
如果存在不想提交到远程仓库的文件，需要在工作区创建.gitignore文件。

    touch .gitignore
    












