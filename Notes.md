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

查看现有版本

> git log
> git log --pretty=oneline

回退曾经版本

> git reset --hard HEAD^^
> git reset --hard HEAD~2

跳转某个版本

> git reset --hard _commit-id_

查看记录改动命令及版本号

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

## 远程仓库

## 分支管理

## 标签管理

## 使用GitHub

## 使用Gitee

## 自定义Git

## 使用SourceTree

## 总结
