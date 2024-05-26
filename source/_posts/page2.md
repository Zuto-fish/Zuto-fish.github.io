---
title: Git
categories: [Git]
tags: [Git]
date: 2021-08-11 16:00:00
---



## 基本使用

````bash
git config --global user.name name
git config --global user.email mail
去掉参数就是查看

git init
初始化,创建版本库

````



使用逻辑

首先是文件分区

我们能直接看到的这个文件夹里面的所有文件就是工作区

初始化后会新建一个*.git*文件夹，这是版本库

git add 是把文件添加到了 暂存区 *stage*

而commit 命令将其提交到了 版本库中




````bash
添加文件或目录到缓存区域
git add <file>
git add . //添加所有

提交缓存区域文件到版本库
git commit -m “what I have done”

git diff 查看做出了哪些修改
git log 产看提交记录 加 --preety=online 简化
````



回退

```bash
git reset --hard HEAD^ 回退一个版本 这里是改指针，可以切回去

取消工作区：
git checkout -- <file> （回到暂存区域，没有--则是版本库）

取消暂存区域
git reset HEAD <file>  删除暂存区域

```



下面是一些分支方面的命令

```
git branch -v  //查看
git branch <branch name> 创建分支

git checkout <branch name>

git merge <branch name>  把指定分支合并到当前分支
```


- 冲突合并
    原因：两处都修改了同一个地方
    现象：会提示你冲突文件，冲突文件会有奇奇怪怪的标记，此时，你会发现自己正处于 MERGING 状态
    解决方案：手动去修改就行了
- git手动更改后，需要的是 commit,这个时候后面就不能带文件名了
    合并完成之后自然也是只会改变当前的这个状态
    启示：Git 底层是head指针



Github

```
git remote  //创建别名
	-v //查看有哪些别名
	add <别名> <库地址> 

操作方面
最基础的俩
git push <仓库（可以用别名）>  <分支>   //这个是推送
git pull <仓库（可以用别名）>  <分支>  //拉取

克隆是不需要登录的

拉取代码，初始化仓库，创建别名-> 一步到位
别名会创建成 origin

```
