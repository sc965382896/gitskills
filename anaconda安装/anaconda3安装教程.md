# anaconda安装教程

该安装过程基于 ubuntu16.04 系统。包含以下部分：

* anaconda 的下载及安装
* anaconda 的常用指令
* pytorch 与 tensorflow 模块的安装示例（其他模块安装方式类似）

## 一、anaconda 的下载及安装

### 1.1 anaconda安装步骤

首先登录https://www.anaconda.com/distribution/#download-section，下载 for Linux 的 Python 3.7 版本，该版本适用于 ubuntu 系统，支持 python 2.7 ，python 3.5-3.7 。

![anaconda_download](/home/sc965382896/Desktop/install_anaconda.png)

打开文件所在文件夹，右键打开终端，键入下列指令：

```
bash Anaconda3-2019.07-Linux-x86_64.sh
```

> 其中文件名更改为下载的文件名。

然后按提示进行安装即可。

当出现“Thank you for installing Anaconda!”，则表明安装完成。此时关闭该终端，在另一个终端中打开以启动Anaconda。

### 1.2 安装成功验证

安装完成后，可以使用下列方式验证：

1. 使用指令conda --version，出现下图表明安装成功。

![](/home/sc965382896/Desktop/version.png)

2. 输入python打开python解释器，出现下图表明安装成功，使用exit()可以退出解释器。

![](/home/sc965382896/Desktop/python.png)

3. 使用anaconda-navigator可以打开anaconda的图形化界面。

## 二、anaconda 的常用指令

### 2.1 环境管理

#### 2.1.0 使用前须知

下面的指令均在Linux的Terminal（终端）中进行操作。

#### 2.1.1 创建新环境

```
conda create --name <env_name> <package_names>
```

* **注意事项：**
  * <env_name> 即创建的环境名。不必包括尖括号“<>”。
  * <package_names> 即安装在该环境的模块名称。同样不包括尖括号，**可以在多个模块名中间加入空格同时安装多个模块**，可以通过在模块名后使用=和版本号形式指定安装的模块版本。
  * 示例：conda create --name new_env python=3.7 numpy

#### 2.1.2 切换环境

```
source activate <env_name>
```

或者

```
conda activate <env_name>
```

#### 2.1.3 显示已创建的环境

```
conda env list
```

![conda_list](/home/sc965382896/Desktop/conda_list.png)

> "*"星号为当前所在的环境。

#### 2.1.4复制环境

```
conda create --name <new_env_name> --clone <copied_env_name>
```

* **注意：**
  * <new_env_name> 即复制后的环境名。同样不包含尖括号。
  * <copied_env_name> 即被复制的环境名。同样不包含尖括号。

#### 2.1.5 退出环境

```
conda deactivate
```

#### 2.1.6 删除环境

```
conda remove --name <env_name> --all
```

* **注意：**
  * <env_name> 即被删除的环境名称。同样不包括尖括号。

### 2.2 包管理

#### 2.2.1 查看当前环境中已安装的包信息

```
conda list
```

#### 2.2.2 查找包

旨在查找是否有可供安装的包

**精确查找**，即按包的全称查找

```
conda search --full-name <package_full_name>
```

**模糊查找**，即查找包含该字段的包

```
conda search <text>
```

#### 2.2.3 安装包

在**指定环境**中安装包

```
conda install --name <env_name> <package_name>
```

在**当前环境**中安装包

```
conda install <package_name>
```

使用pip安装包，当 conda 无法进行安装时，可以采用这种方式

```
pip install <package_name>
```

#### 2.2.4 卸载包

卸载**指定环境**中的包

```
conda remove --name <env_name> <package_name>
```

卸载**当前环境**中的包

```
conda remove <package_name>
```

#### 2.2.5 更新包

更新**所有**包

```
conda update --all
```

或者

```
conda upgrade --all
```

更新**指定**包

```
conda update <package_name>
```

或者

```
conda upgrade <package_name>
```

## 三、pytorch 和 tensorflow 安装示例

### 3.1 pytorch 安装

创建环境：

```
conda create --name pytorch python=3.7 pytorch
```

![pytorch](/home/sc965382896/Desktop/pytorch.png)

输入y，回车即可完成安装。

> 这里并未指定安装的 pytorch 版本，具体根据需要安装 pytorch 及 python 版本。

安装完成后切换到该环境中：

```
conda activate pytorch
```

### 3.2 tensorflow 安装

创建环境：

```
conda create --name tensorflow python=3.7 tensorflow
```

> 这里需要注意的是，如果安装 gpu 版本，需要将 tensorflow 替换为 tensorflow-gpu。

待搜索包结束后，输入y，回车后等待下载安装完成即可。

安装完成后切换到该环境中：

```
conda activate tensorflow
```
