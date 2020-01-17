# Git 配置

Git 提供了 **git config** 工具，用来配置或读取相应的工作环境变量。

## 配置用户信息

* 配置用户名：**git config --global user.name (name)**
* 配置用户邮箱：**git config --global user.email (email_addr)**

## 查看配置信息

**git config --list**

# 工作区、暂存区和版本库

* **工作区：**电脑中的目录
* **暂存区：**也叫**stage**，或**index**。一般存放在**.git目录**（隐藏目录）下的index文件中
* **版本库：**工作区中的隐藏目录 **.git** ，不算工作区，而是 Git 的版本库

![工作区和版本库的关系](images/工作区和版本库的关系.jpg)

# 创建仓库

## git init 

使用当前目录作为 Git 仓库，只需要将其**初始化**

* **git init：**将当前目录初始化为 Git 仓库

## git clone

* **git clone \<repo\>：**克隆指定的 Git 仓库
* **git clone \<repo\> \<directory\>：**克隆指定的 Git 仓库到某个目录下

**参数说明：**

* **repo：**Git 仓库
* **directory：**本地目录名

# 基础操作

## git add

执行 **git add** 命令可以将文件添加到**缓存**。

* **git add \<file\>：**添加文件名为 file 的文件到缓存
* **git add .：**添加所有新增文件到缓存，包括文件夹
* **git add *.c：**添加后缀为 .c 的文件到缓存

## git status 

**git status** 命令用来查看上次提交后是否有更改及更改的内容。

* **git status：**查看更改内容
* **git status -s：**查看简短的状态

简短状态的各个**符号含义**：

* **？：**表示没有被 track（跟踪）的文件更改
* **A：**表示新增的文件
* **M：**表示修改的文件
* **D：**表示删除的文件

## git diff

**git diff** 命令显示 **git status** 的**详细信息**。

- **git diff：**尚未缓存的改动
- **git diff --cached： **查看已缓存的改动
- **git diff HEAD：**查看已缓存的与未缓存的所有改动
- **git diff --stat：**显示摘要而非整个 diff

## git commit

执行 **git add** 写入缓存后，执行 git commit 将缓存区内容添加到**仓库**中。

常见选项：

* **-m：**提供提交注释，没有该选项时会尝试打开编辑器填写提交信息
* **-a：**修改文件后，跳过缓存，直接提交到仓库
* **-am/-a -m：**同时执行以上两个步骤

## git reset 

**git reset** 命令取消已缓存的内容。

* **git reset \<file\>：**取消文件 file 的缓存

## git reset HEAD

执行 **git reset HEAD** 命令用当前分支的版本库目录替代缓存区目录。

* **git reset HEAD \<file\>：**用版本库中的文件替代缓存区的文件

## git rm

**git rm** 命令将文件从已跟踪文件清单中移除。

> 已跟踪文件的含义：已经添加到缓存区中的文件，包含上次版本库中的，以及本次 add 到缓存区中的文件。

* **git rm \<file\>：**删除缓存区和工作目录中的文件
* **git rm -f \<file\>：**当工作目录与缓存区中文件内容不一致时，需要使用 -f 选项
* **git rm --cached \<file\>：**仅从跟踪清单中删除文件
* **git rm -r *：**递归地删除目录下的所有子目录和文件

## git mv

**git mv** 命令用于移动或重命名一个文件、目录、软连接。

## git checkout \<file\>

执行 **git checkout \<file\>** 命令从缓存区中恢复文件。

## git checkout HEAD \<file\>

执行 git checkout HEAD \<file\> 命令从版本库中恢复文件。

# 分支管理

分支会保存最近提交的快照，切换时替换工作目录的内容，所以不需要多个目录。

**git branch** 命令能列出所有的分支

## git branch

* **git branch (branchname)：**创建分支
* **git branch -d (branchname)：**删除分支
* **git branch -D (branchname)：**强制删除分支（未合并的分支）

## git checkout (branchname)

* **git checkout (branchname)：**切换分支
* **git checkout -b (branchname)：**创建分支并切换

## git merge

**git merge** 命令用于将某分支合并到主分支

## BUG分支(保存现场)

当发现BUG需要进行修复，但工作尚未完成，可以使用下列命令来保存当前的现场：
\$ git stash
修复BUG时需要明确在哪个分支上进行修复，并在其上创建临时分支，修复完毕后合并分支并删除
\$ git stash apply #恢复现场但不删除stash内容
\$ git stash drop #删除stash内容
\$ git stash pop #恢复的同时删除stash内容
\$ git stash list #查看stash内容

> 可以多次stash，然后恢复指定的stash

# 查看提交日志

**git log** 命令回顾提交历史。

* **git log -oneline：**查看简洁的提交历史
* **git log --graph：**查看拓扑图，哪里出现分支和合并
* **git log --reverse：**逆向显示历史
* **git log --author：**查看某个用户的提交日志
* **--since --before --until --after：**前两个是时间长度，后两个是具体时间，如--before={3.weeks.ago}，--after={2010-04-18}
* **git log --decorate：**查看含标签的日志

# 标签

**git tag** 命令添加标签，通常使用带注解的标签：

* **git tag -a (tagname)：**执行后打开编辑器，添加一句**标签注解**
* **git tag -a (tagname) (lognum)：**发布了某个版本后，使用这个命令**追加**标签
*  **git tag -d (tagname)：**删除标签
* **git tag：**查看所有标签

# 创建远程仓库

## 添加远程库

1. 创建 SSH Key
  * **ssh-keygen -t rsa -C "email_addr"：**在用户主目录中创建 SSH Keyb
2. 复制 **.ssh** 文件夹下的 **-id_rsa.pub** 中**SSH**，在 github 中添加 SSH Key
3. 提交到 GitHub
   * **git remote add origin git@github.com:x/x.git：**添加远程仓库
   * **git push -u origin mastre：**推送到远端分支

## 远程库操作

### 查看远程库

* **git remote：**查看当前配置的远程库
* **git remote -v：**查看远程库各个别名的链接地址

### 提取远程库

* **git fetch [alias] [branch]：** 提取远程仓库 alias 上的分支到本地
* **git merge [alias]/[branch]：**将从远程仓库提取的分支合并到当前分支上

### 推送远程库

* **git push [alias] [branch]：**推送 [branch] 分支到远程仓库 [alias] 的 [branch] 分支

### 删除远程库

* **git remote rm [alias]：**删除远程仓库 [alias]

# 分支管理

## 禁用Fast forward模式   
\$ git merge --no-ff -m "merge with no-ff" dev #--no-f参数为禁用Fast forward，-m用于描述commit

## 抓取分支

\$ git checkout -b dev origin/dev #在本地创建远程origin的dev分支
\$ git pull #抓取远程库中最新的提交并尝试合并

> 如果git pull失败，则根据提示设置dev和origin/dev的链接

\$ git rebase #将本地未push的分支提交历史整理成直线
> 只对尚未推送或分享给别人的本地修改执行变基操作清理历史；从不对已推送至别处的提交执行变基操作

## 标签

$ git push origin <tagname> #推送单个标签 
​\$ git push origin --tags #推送全部尚未推送至远程的本地标签 
\$ git push origin :refs/tags/<tagname> #删除一个远程标签

# linux 文件操作指令

```
cd <foledr name> # 载入目录

ls # 浏览目录下的文件
ls -a # 浏览目录下的所有文件（包括隐藏文件）

cat <file name> # 打开文件

pwd # 显示当前位置

mkdir <filename> # 创建目录
```



