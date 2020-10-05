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

有时候会进行FastForward模式合并，直接把当前分支指向目标分支。

## 标签管理

## 使用GitHub

## 使用Gitee

## 自定义Git

## 使用SourceTree

## 总结
master
dev
