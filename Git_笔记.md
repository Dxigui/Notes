# Git 笔记 #

## Git 简介##

Git 是开源的分布式版本控制系统，由 Linus 开发，去中心服务器，每个人都有完整的代码，能够在离线状态下进行修改，还有其强大的版本控制系统，它跟踪并管理的是用户的修改而非文件。除了 Git 外还有 Mercurial、Bazaar 等分布式版本控制系统。

既然有分布式，那就有集中式版本控制系统，但是集中式只有一个中心服务器，安全性能差，只能在联网条件下修改代码，且速度较慢。代表有 SVN、ClearCase 等。

## Git 安装##

### Linux ###

```ubuntu
# ubuntu
gx@loaclhost:~$ apt-get install git
# 如果权限不够，会提示输入密码
gx@loaclhost:~$ sudo apt-get install git

# CentOS
[root@loaclhost ~]# yum install git
```

### Windows

[官网](https://git-scm.com/downloads) 下载 Windows 版本，全部默认安装就行

安装完成后进入 Git Bash ，设置用户名和邮箱，让别人能识别你的主机。

```git
# 设置用户名
$ git config --global user.name "Your name"
# 设置邮箱
$ git config --global user.email "email@example.com"
```

`--global`  参数表示这台机器上所有 Git 仓库都使用这个用户名和邮箱。也可以指定不同仓库使用不同用户名和邮箱，在你需要设定的仓库下面执行上面的 `git config`  命令，但是不加 `--global`  参数。

## Git 使用 

###  创建分支

后面的都是基于 Ubuntu

创建一个项目文件

```
$ mkdir learngit
```

跳转到项目文件里面

```
$ cd learngit
```

初始化，让改目录变成能够被 Git 管理的目录

```
$ git init
# 出现成功创建的提示 并显示其目录地址
# 该目录下多一个 .git 文件 
```

创建一个新文件，输入内容后把他提交到 Git

```
# 创建测试文件夹
$ touch readme.txt

# 输入内容
$ vim readme.txt
This is a git file
Git is a version control system

# 将刚刚创建并修改的文件添加到缓存区
$ git add readme.txt

# 将缓存区中的文件提交到 Master 分支
# -m 是为这次提交进行注释
$ git commit -m "test file"
```

### 查看工作区状态和文件修改内容

使用 `git status`  命令查看各个工作区状态以及是否有文件别修改。

```
# 修改文件
$ vim readme.txt
Git is a distributed version control system

# 如果文件存在且被修改，提示该文件被修改
# 当有新文件创建时，提示新文件
$ git status
// 提示文件已经被修改

# 查看文件别修改的内容
$ git diff readme.txt
// 文件被修改的地方，修改后会和修改前对比
diff --git a/readme.txt b/readme.txt
index 6bf6290..7ba75af 100644
--- a/readme.txt
--- b/readme.txt
@@ -1,4 +1,4 @@
-Git is a version control system
+Git is a distributed version control system
This is a git file
Git is a version control system

# 查看工作区和版本库中最新版本的区别，
# 在此之前需要了解版本库和工作区
$ git diff HEAD -- readme.txt
```

### 版本切换/回滚

查看提交日志

```
$ git log
// 完整的提交日志
commit 6c99063855e6c5492f8dc49c3c3ae8022d764afa
Author: Dxigui <xingbake95@gmail.com>
Date:   Mon Jul 16 15:36:24 2018 +0800

    add distributed

commit 9f691ca145f259a4d95ab46d634a21b95bd5eece
Author: Dxigui <xingbake95@gmail.com>
Date:   Mon Jul 16 15:06:16 2018 +0800

    add a line

commit 6030ae8b488a6ca1e81a0b6717d6be486992d46b
Author: Dxigui <xingbake95@gmail.com>
Date:   Mon Jul 16 14:41:46 2018 +0800

```

简化提交日志

```
$ git log --pretty=oneline
// 添加 --pretty=oneline 参数简化提交日志
6c99063855e6c5492f8dc49c3c3ae8022d764afa add distributed
9f691ca145f259a4d95ab46d634a21b95bd5eece add a line
6030ae8b488a6ca1e81a0b6717d6be486992d46b test file

```

每个版本是通过 commit id 来识别的，Git 中用 HEAD 表示当前版本，时最新提交的 id ，上一个版本为 HEAD^，上上个版本为 HEAD^^ 

版本回滚

```
# 回到上一个版本
$ git reset --hard HEAD^
//
HEAD is now at 9f691ca add a line
```

知道 commit id 才能切换版本

### 工作区和暂存区

最开始创建的 learn_git 文件夹在初始化后这个目录就是一个工作区，这个文件夹中的 .git 是 Git 的版本库。

在版本库中包含有 stage（暂存区），master 分支以及一个指向 master 分支的 HEAD 指针。

我们修改、创建的文件初始位置就是在工作区中，在执行 `git add <filename> `  后，Git 就会把工作区中创建或者修改的文件添加到 stage （暂存区）中，在暂存区中的文件在执行 `git commit`  提交后，将暂存区中的所有内容提交到当前分支。所以，想要把文件提交到版本库中只要进行两部操作就可以了。

实例：对一个文件先后进行两次修改，对前一次修改添加到暂存区，而后一次不做处理，然后进行 `git commit`  ，会发现 Git 只把第一次修改提交到了分支，而第二次修改还在工作区。

### 撤销修改

1. 需要撤销的内容在工作区

```
# 撤销工作区中的所有修改
# 可以让文件回到最近一次 git add 或 git commit
# git checkout 是让版本库中的版本覆盖工作区
$ git checkout -- <file name>
```

2. 需要撤销的内容在暂存区

```
# 把暂存区的修改退回工作区
$ git reset HEAD <file name>
# 将退回工作区的修改撤销
$ git checkout -- <file name>
```

3. 需要撤销的内容在版本分支

```
# 回滚到上一个版本
$ git reset HEAD^ <file name>
```

### 删除文件

文件管理器删除和用 Git 删除，两者先后顺序不影响。

```
# 在 rm file 后只是删除了工作区的文件，版本库中还没有被删除
# 要删除版本库中的使用下面两条命令
$ git rm <file name>
$ git commit -m "delect file"

# 既然工作区的文件被删了后版本库还有的话
# 那么误删了工作区的文件就容易被恢复了
# 使用 git checkout 用版本库覆盖工作区
$ git checkout -- <file name>
```

## 远程仓库

### 建立远程仓库连接

* 注册 GitHub 账号
* 生成 SSH Key

```
# 生成 SSH Key
$ ssh-keygen -t rsa -C "Youremail@exmpale.com"
```

* 将 SSH Key 添加到 GitHub 上去

### 生成远程仓库并推送和克隆

先在 GitHub 上创建一个新的远程仓库，然后关联本地仓库。

```
# 远程仓库与本地关联
$ git remote add origin git@gitgub.com:Dxigui/Notes

# 移除关联
$ git remote rm origin
```



