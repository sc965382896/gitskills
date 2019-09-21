# Ubuntu
## 1 Ubuntu安装
### 1.1 制作U盘安装
* 由官网下载，使用官网推荐的软件写入U盘中。

* 插入U盘，使用U盘启动，按照提示完成安装。

## 2 Ubuntu中软件安装
### 2.1 安装命令command
* sudo apt-get install XXXX 安装软件。

* sudo apt-get remove XXXX 删除已安装的软件包，不会删除依赖软件包，保留配置文件。

* sudo apt-get autoremove 删除为了满足依赖而安装的，但现在不再需要的软件包，保留配置文件。

## 3 Ubuntu基础指令
### 3.1 ls和cd
#### 3.1.1 cd
* cd XX/XX/为移动到某文件位置。

* cd ..返回上一级目录。

* cd -返回之前所在的目录。

* cd ../../../可以返回多级目录。

#### 3.1.2 ls
* ls 浏览当前目录下的所有文件。

* ls -l 文件的详细信息。

* ls -a 显示所有文件（包含隐藏文件）。

* ls -lh 以方便人看的方式浏览文件。

### 3.2 touch cp mv
#### 3.2.1 touch 
* touch file1 file1后面可以添加后缀。

#### 3.2.2 cp
* cp old_file new_file 当前文件夹下进行拷贝。

* cp -i old_file new_file 带有报错的copy。

* cp file1 folder1/ 拷贝到当前目录下的文件夹中。

* cp -r folder1/ folder2 把文件夹中的拷贝到另一个文件夹中。

* cp file* folder2/ 拷贝前缀为file的所有文件。

* cp file1 file2 folder2/ 同时拷贝多个文件，目标必须为文件夹。

#### 3.2.3 mv
* mv file1 folder1/ 将文件移动到某文件夹。

* mv file1 file1rename 实现重命名操作。

### 3.3 
