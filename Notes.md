# 廖雪峰Git笔记

## 创建版本库

创建本地仓库
> git init

把工作区文件添加到版本库
> git add _file_  
> git commit -m "_msg_"

## 时光机穿梭

掌握仓库当前状态
> git status

比较未add的修改内容
> git diff _file_

### 版本回退

查看现有版本（现有时间线）

> git log  
> git log --pretty=oneline

回退曾经版本
> git reset --hard HEAD^^  
> git reset --hard HEAD~2

跳转某个版本
> git reset --hard _commit-id_

查看记录改动命令及版本号（对时间线做的每一个变动）
> git reflog

注意！  
**切换版本会丢失工作区修改和暂存区内容！即完全复制上一次commit的状态！**

### 工作区和暂存区

名词解释

- 工作区：电脑中可见的目录
- 版本库：.git目录，包含暂存区stage，分支如master，以及指针HEAD

操作解释

- git add 是把文件修改添加到暂存区
- git commit 是把暂存区内容提交到当前分支

### 管理修改

git跟踪并管理的是修改而非文件（git只能判断出纯文本文件的修改，诸如word或jpg都不行）

比较工作区文件与某版本该文件的区别
> git diff HEAD^ -- _file_

### 撤销修改

恢复工作区到最近add/commit时的状态
> git checkout -- _file_

撤销暂存区修改
> git reset HEAD _file_

### 删除文件

先手动删除，之后执行命令之一：
> rm _file_  
> git rm _file_  
> git add _file_  
> git commit -m "_msg_"

如果误删且没有add，则恢复：
> rm _file_  
> git checkout -- _file_

## 远程仓库

### 添加远程库

关联远程仓库
> git remote add origin _url_

推送本地内容某分支到远程库该分支（第一次加-u）
> git push origin _branch_

### 从远程库克隆

根据远程库，在当前目录下，克隆生成本地库
> git clone _url_

## 分支管理

### 创建与合并分支

HEAD指向当前所在分支，分支指向当前分支线的提交点。

创建分支
> git branch _br_

切换分支
> git checkout _br_  
> git switch _br_

创建并切换到新分支
> git checkout -b _br_  
> git switch -c _br_

列出所有分支
> git branch

将某一分支合并到当前分支
> git merge _br_

删除分支
> git branch -d _br_

有时候会进行FastForward模式合并，直接把当前分支指向目标分支。（这种方式使得流程不清晰）

### 解决冲突

git冲突会产生于多个分支修改了同一个文件后合并时（push和pull是合并本地和远程分支），在不同分支中修改不同文件不会有冲突，所有修改都会保留。

解决方法：合并后会在工作区自动产生修改，自己修改解决冲突之后，可以add&commit提交修改。

查看分支合并情况
> git log --graph

### 分支管理策略

git在合并时会尽可能使用FastForward模式，但容易丢失信息。

强制禁用FastForward模式（会创建新节点，需要-m信息）
> git merge --no-ff -m "_msg_" _br_

- master分支应当稳定，一般仅用来发布新版本
- dev分支可以是不稳定的，平时可干活，做好了合并到master
- name分支是每个人个人分支，可以时不时向dev合并

### Bug分支

在进行工作时，若发现之前版本有bug，则可以新建分支进行修复，之后合并分支，并在其他分支进行修改。

工作区和暂存区有修改未提交或未保存时，无法切换分支。

保存工作区和暂存区修改
> git stash

查看保存的工作现场
> git stash list

恢复工作现场
> git stash apply

删除工作现场
> git stash drop

恢复并删除工作现场
> git stash pop

复制一个特定的提交（算作另一次新提交）
> git cherry-pick _commit-id_

### Feature分支

开发一个新功能，可以新建一个分支。

强制删除未被合并的分支
> git branch -D _br_

### 多人协作

查看远程库信息（-v查看详细信息）
> git remote

推送本地该分支所有提交到远程库的分支
> git push origin _br_

- master为主分支，应时刻和远程同步
- dev为开发分支，所有成员在其上工作，需要和远程同步
- 个人分支一般不用，视情况而定

克隆远程库，默认只克隆master分支。  
创建远程的分支到本地：
> git checkout -b _br_ origin/_br_

在多方在同一分支上某一文件进行了修改，并有人线性推送该分支的提交，则后推送的会产生冲突。  
此时应当拉取最新的提交，解决冲突后再推送。

设定本地分支与远程分支的链接
> git branch --set-upstream-to=origin/_br_ _br_

从远程库拉取同名分支到当前分支
> git pull

从远程库拉取指定分支到当前分支
> git pull origin _br_

### Rebase

把分叉的提交变为直线
> git rebase

它把分支的提交历史变为直线，看上去更直观，但会丢失分叉信息。

比较复杂，暂不展开叙述。

## 标签管理

标签是某个版本库的快照，它实际是指向某个提交的指针，且不能移动。tag就是一个有意义的名字，和某个commit绑定到一起。

### 创建标签

查看当前分支的所有标签（字母排序）
> git tag

在当前分支当前节点打标签
> git tag _tag_

为当前分支指定提交打标签
> git tag _tag_ _commit-id_

创建带有说明的标签
> git tag -a _tag_ -m "_msg_" _commit-id_

查看指定标签信息
> git show _tag_

### 操作标签

删除本地标签
> git tag -d _tag_

推送标签到远程
> git push origin _tag_

推送全部未推送的标签
> git push origin --tags

删除远程标签（推送空标签到指定标签）
> git push origin :ref/tags/_tag_

## 使用GitHub

Fork从别人远程仓库克隆到自己远程仓库，再clone从自己远程仓库到自己本地仓库，这样修改可以提交到自己的远程仓库。

需要别人接受你的修改，可以发起一个 pull request.

## 使用Gitee

## 自定义Git

## 使用SourceTree

## 总结
