[TOC]

# Git 学习指南

## 第1章 基本概念

### 1.1 分布式版本控制

集中式版本控制系统(CVS Subversion)， 每个开发者都在自己的计算机上有一个包含所有项目文件的工作目录，即工作区。

在分布式版本控制系统中，开发者环境与服务器环境之间是没有分隔的。通过push和pull命令，可以将修改从一个版本库传送到另一个版本库中。

分布式系统相对于集中式的优点：

**高性能**

**高效的工作方式**

**离线功能**

**灵活的开发进程**

**备份作用**

**可维护性**



### 1.2 版本库，分布式工作的基础所在

版本库本质上是一个高效的数据存储结构而已，由**文件 blob ** **目录 Tree** **版本 Commit** 组成。



### 1.3 分支的创建与合并

在Git中，可以开启有针对性的分支，即显式的创建一个分支，通常主要用于协调某一种功能性的并行开发。



## 第2章 入门

### 2.1 准备Git环境

[git官网][http://git-scm.com/download]

可以使用```git config``` 配置用户名和用户邮箱。

### 2.2 第一个Git项目

#### 2.2.1 创建版本库

~~~shell
git init
~~~



#### 2.2.2 首次提交

```shell
git add xxx
git commit -m "commit message"
```

#### 2.2.3 检查状态

```shell
git status
```

```shell
git diff xxx
```

通过git diff命令可以具体显示每个被修改的行。

#### 2.2.4 提交修改

~~~shell
git add xxx
git rm xxx
~~~

#### 2.2.5 显示历史

~~~shell
git log
~~~

这条命令可以显示项目的历史，所有的提交都会按照时间顺序排列出来。

### 2.3 Git的协作功能

在Git中，每位开发者拥有一个属于他自己的、自带独立版本库的工作区。

#### 2.3.1 克隆版本库

~~~shell
git clone "url"
~~~

#### 2.3.2 从另一版本库中获取修改

~~~shell
git pull
~~~

~~~shell
git log --graph
~~~

#### 2.3.3 从任意版本库中取回修改

~~~shell
git pull <远程主机名> <远程分支名>:<本地分支名>
~~~

#### 2.3.4 创建共享版本库

push命令只适用于那些没有开发者在上面开展具体工作的版本库。

创建一个不带工作区的版本库，称之为裸版本库（bare repository）。

```shell
git clone --bare /url
```

裸版本库可以被用来充当开发者们传递提交push的汇聚点，以便其他人可以从中拉回他们所做的修改。

#### 2.3.5 用push命令上载修改

~~~shell
git push path branch
~~~

#### 2.3.6 Pull命令：取回修改

git pull <远程主机名> <远程分支名>:<本地分支名>



## 第3章 提交究竟是什么

### 3.1 访问权限与时间戳

Git会保存每个文件的访问权限，但不会保留文件的修改时间。

### 3.2 add命令与commit命令

### 3.3 再谈提交散列值

```shell
git fsck
```

查看版本库的完整性

~~~shell
git checkout HASH
~~~

切换到某个版本

### 3.4 提交历史

形成关系图。

### 3.5 一种略有不同的提交查看方法

版本库实际上是一部项目的修改历史。

```shell
git diff
(1) git diff HASH HEAD
(2) git diff HASH^! ^!的意思是比较和上一次提交之间的差异
(3) git diff --stat 显示每个文件中的修改数量
```

### 3.6 同一项目的多部不同历史

#### 3.6.1 部分输出 -n

```shell
git log -n 3 显示该项目最后3次提交
```

#### 3.6.2 格式化输出

```shell
git log --format
--format=fuller 显示许多细节信息
--oneline 显示概述信息
```

#### 3.6.3 统计修改信息

``` shell
--shortstat显示项目中有多少文件被修改，以及新增或删除了多少文件
--dirstat 显示包含被修改文件的目录
--stat显示被修改的那些文件
```

## 第4章 多次提交

### 4.1 status命令

```shell
git status (--short) # --short命令可以使得相关输出显得更加紧凑
```

显示 被提交的修改、不会被更新的修改、未被跟踪的文件

### 4.2 存储在暂存区中的快照

```shell
git diff --staged # 所显示的是当前版本库中HEAD提交与暂存区之间的不同之处
```

### 4.3 怎样的修改不该被提交

```shell
git reset HEAD .
```

### 4.4 用.gitignore忽略非版本控制文件

使用项目目录下的.gitignore文件。

### 4.5 储藏

~~~shell
git stash #将工作区和暂存区的修改保存在一个stack缓存中
git stash pop # 恢复栈顶的修改
git stash list
git stash pop stash@{1} #恢复某个更早的修改
~~~

