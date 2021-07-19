## Git

### 一、Git介绍

Git 是一个开源的分布式版本控制系统

Git 和其它版本控制系统(包括 Subversion 和近似工具)的主要差别在于 Git 对待数据的方式。 从概念上来说，其它大部分系统以文件变更列表的方式存储信息，将它们存储的信息看作是一组基本文件和每个文件随时间逐步累积的差异 (它们通常称作 **基于差异** (**delta-based**) 的版本控制)。

Git 不按照以上方式对待或保存数据。反之，Git 更像是把数据看作是对小型文件系统的一系列快照。 在 Git 中，每当你提交更新或保存项目状态时，它基本上就会对当时的全部文件创建一个快照并保存这个快照的索引。 为了效率，如果文件没有修改，Git 不再重新存储该文件，而是只保留一个链接指向之前存储的文件。 Git 对待 数据更像是一个 **快照流**。



#### Git 文件状态

 在Git 版本库中有三种状态，文件有三种状态: **已提交(committed)**、**已修改(modified)** 和 **已暂存(staged)**。

如果在本地工作区中文件📁只有两种状态：**已跟踪(Tracked)** 或 **未跟踪(Untracked)**，已跟踪状态就包括以上三种文件状态

- 已修改表示修改了文件，但还没保存到数据库中。

- 已暂存表示对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中。

- 已提交表示数据已经安全地保存在本地数据库中。

![git文件状态](https://tva1.sinaimg.cn/large/008i3skNgy1gsmgit7po8j314g0hsq46.jpg)



#### Git 工作区、暂存区和版本库

由以上的三种文件状态引出 Git 中三个“区”：工作区、暂存区和版本库

- 工作区是对项目的某个版本独立提取出来的内容，也就是我们通俗意义上的本地仓库目录
- 暂存区(stage)是一个文件，保存了下次将要提交的文件列表信息，一般在 Git 仓库目录中
- Git 仓库目录是 Git 用来保存项目的元数据和对象数据库的地方，也就是对应我们工作区目录下的 .git 隐藏文件夹

![工作区暂存区版本库](https://tva1.sinaimg.cn/large/008i3skNgy1gsmghgwrllj315u0m6q4f.jpg)

如果 Git 目录中保存着特定版本的文件，就属于 **已提交** 状态。 如果文件已修改并放入暂存区，就属于 **已暂存** 状 态。 如果自上次检出后，作了修改但还没有放到暂存区域，就是 **已修改** 状态。

![工作区与版本库](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/image-20191208195941661.png)



### 二、常用Git命令及其含义 

下面将从从拉去项目到提交代码远程仓库对常见 Git 命令及其含义进行介绍

#### git clone

假设我们已经在 Gitlab 或者 GitHub 上有项目的代码，使用`git clone`命令将项目从远程仓库**克隆**到本地

```shell
$ git clone <repo-url>                      # <repo-url>为远程仓库地址
$ git clone <repo-url> <local-repo_name>    # <local-repo_name>为自定义本地仓库名字
$ git clone https://github.com/spring-projects/spring-boot.git  my-spring
```



#### git add 

拉去到项目之后进行了一些列的开发，执行`git add`命令将本地工作区的代码提交到暂存区(stage)

```shell
$ git add --all/-A 													 # 添加当前项目下的所有更改到暂存区
$ git add .        													 # 添加当前目录下的所有更改到暂存区
$ git add <file-name1> <file-name2>				   # 添加某些文件的更改到到暂存区
```



#### git commit 

使用`git commit `命令把暂存区的修改提交到当前分支，提交之后暂存区就被清空了

```shell
$ git commit -m "<commit-message>"           # 将暂存区所有修改提交到当前分支的版本库，清空暂存区
```



#### git push

现在我们已经将所有的修改都添加到本地仓库了，现在需要将本地的修改推送的远程仓库中

```shell
$ git push -u <remote-name> <remote-branch-name>   # 把本地修改提交到远程仓库，第一次需要关联上远程仓库名和分支名
$ git push 																			   # 之后再推送就不用指明应该推送的远程分支了
```















































































#### git status

主要查看文件在工作区、暂存区、本地仓库三者之间的状态

```shell
$ git status 															 # 查看文件在工作区、暂存区、本地仓库三者之间的状态
$ git status --short/-s										 # 用一种更精简的方式输出当前仓库文件的状态
```





















#### git branch 

Git 的分支也非常轻量。它们只是<u>简单地指向某个提交纪录</u> —— 仅此而已。

在将分支和提交记录结合起来后，我们会看到两者如何协作。现在只要记住使用分支其实就相当于在说：“我想基于这个提交以及它所有的父提交进行新的工作。”

```shell
$ git branch <branch-name>    							# 新建名为<branchname>的新分支
$ git checkout <branch-name>  							# 切换工作区到<branchname>分支
$ git checkout -b <branch-name> 						# 新建<branchname>的新分支，并切换到<branchname>分支上
```

可以直接使用 `-f` 选项让分支指向另一个提交。例如:

```
git branch -f main
```

#### git merge



#### git rebase

第二种合并分支的方法是 `git rebase`。Rebase 实际上就是取出一系列的提交记录，“**复制**”它们，然后在另外一个地方逐个的放下去。

Rebase 的优势就是可以创造更线性的提交历史，这听上去有些难以理解。如果只允许使用 Rebase 的话，代码库的提交历史将会变得异常清晰。



