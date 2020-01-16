# 安装Git

安装完成后打开git，然后进行以下操作：

1. 配置用户名 
   $ git config --global user.name "XX"
2. 配置用户邮箱
   \$ git config --global user.email "X@X"

# 创建版本库

新建文件夹
\$ mkdir learngit
进入待定位置
\$ cd learngit
显示当前位置 
\$ pwd

初始化仓库

$ init

> 可以用资源管理器打开文件夹，然后使用右键->Git Bash Here，快速定位到当前文件夹并打开git。

# 添加文件到仓库

添加文件到仓库 
\$ git add 、\<file\>

添加所有文件到仓库

\$ git add .

提交文件到仓库 
\$ git commit -m "XX" #-M "XX"为修改内容的说明

# 查看仓库状态

查看仓库当前的状态 
$ git status
查看文件做了什么修改 
\$ git diff\ <file\>... 
提交修改到仓库
\$ git add \<file\>    

# 版本回退

查看历史记录
\$ git log #命令显示从最近到最远的提交日志
查看文件内容
\$ cat \<file\>

回退到上个版本（前提是没有推送到远程库
$ git reset --hard HEAD^ \#工作区文件内容会改变，修改HEAD^为上一个，HEAD^^上两个，HEAD~100上一百个
查看历史命令
\$ git reflog

\$ git add <file> #是将文件添加到暂存区，文件修改后的内容不执行该命令不会被提交到仓库内

\$ git checkout -- <file> #如果未将修改提交到暂存区，该命令可以将**修改后的文件**回退到上一次add或者commit时的状态
\$ git reset HEAD \<file\> #如果将修改提交到了暂存区，该命令可以回退到上个版本库的状态

> git reset HEAD \<file\>和git reset --hard HEAD的不同：前者仅撤销暂存区的修改，后者会撤销工作区的修改

# 创建远程仓库

1. 创建SSH Key
$ ssh-keygen -t rsa -C "email" #在用户主目录中创建SSH Key
2. 在github中添加SSH Key
3. 关联远程库和本地库
$ git push -u origin master #把原始分支推送到远程库并且将两者关联(-u参数)，之后可以省略-u

# 克隆远程库

1. 在github中创建远程库

2. 在git中输入命令：git clone ...

   > 点击repository界面的clone or download，可以获取...的内容。

# 分支管理

> 每次提交(commit)后，master分支的指针就前移动一步，实质是HEAD指向当前分支

\$ git branch dev #创建dev分支
$ git checkout dev #切换到dev分支
这两个命令相当于：\$ git checkout -b dev

\$ git branch #会列出所有的分支，当前分支前会有 * 号
\$ git merge dev #将dev分支合并到当前分支
\$ git branch -d dev #删除dev分支

## 禁用Fast forward模式   
\$ git merge --no-ff -m "merge with no-ff" dev #--no-f参数为禁用Fast forward，-m用于描述commit

## BUG分支(保存现场)

当发现BUG需要进行修复，但工作尚未完成，可以使用下列命令来保存当前的现场：
\$ git stash
修复BUG时需要明确在哪个分支上进行修复，并在其上创建临时分支，修复完毕后合并分支并删除
\$ git stash apply #恢复现场但不删除stash内容
\$ git stash drop #删除stash内容
\$ git stash pop #恢复的同时删除stash内容
\$ git stash list #查看stash内容

> 可以多次stash，然后恢复指定的stash

## 强制删除分支   

\$ git branch -D <branch-name> #强制删除未合并的分支

## 推送分支

\$ git remote #查看远程库的信息
\$ git remote -v #查看远程库的详细信息
\$ git push origin master #把master分支推送到远程库中的对应分支

## 抓取分支

\$ git checkout -b dev origin/dev #在本地创建远程origin的dev分支
\$ git pull #抓取远程库中最新的提交并尝试合并

> 如果git pull失败，则根据提示设置dev和origin/dev的链接

\$ git rebase #将本地未push的分支提交历史整理成直线
> 只对尚未推送或分享给别人的本地修改执行变基操作清理历史；从不对已推送至别处的提交执行变基操作

## 标签

\$ git tag <tagname> #用于新建一个标签，默认是HEAD，也可以指定一个commit id
\$ git tag -a <tagname> -m "blablabla..." #用于指定标签信息
\$ git tag #查看所有标签
\$ git tag -d <tagname> #删除标签
\$ git push origin <tagname> #推送单个标签 
​\$ git push origin --tags #推送全部尚未推送至远程的本地标签 
\$ git push origin :refs/tags/<tagname> #删除一个远程标签