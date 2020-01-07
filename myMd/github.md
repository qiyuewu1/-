# github

## 一、git的使用

### 1、安装

默认安装。。。

### 2、设置标识

`git config --global user.name "sunyuhong"`

`git config --global user.email "sunyh0w0@163.com"`

### 3、创建仓库

- `E:\gitRepository>git init`   在指定目录下初始化仓库

- 没有指示文件夹就代表 前边**E:\gitRepository**的路径为git的版本仓库

### 4、提交

- 在仓库中的文件，执行`git add readme.md ` 放至**暂存区**中
- 再执行`git commit -m "这里写这次提交的备注"` 提交至仓库中
- 这时可以查看本地仓库的状态`git status` 。

### 5、修改

- 查看修改后与之前的不同 `git diff readme.md`  
- 继续add，commit操作

### 6、版本回退

- `git log` 查看当前仓库的提交日志 
- `git log -pretty=oneline` 简化输出日志
- `git reset --hard HEAD^` 回退到上一个版本
- `git reset --hard HEAD^^^`  回退前三个版本
- `git reset --hard HEAD~50`  回退前五十个版本

### 7、恢复回退的内容

- `git reflog` 获取版本号（第一列 16进制数）
- `git reset --hard 6f6cfc89`  恢复到这个版本的内容

### 8、撤销修改

- 通过`git status`查看到当前修改有误
- 使用`git checkout -- readme.txt` 可将未提交到暂存区中的内容撤销掉

### 9、删除后提交与恢复

- 这里的删除，指的是在工作区中的删除

- 删除文件后，commit可同步到仓库
- 或者`git checkout --文件名` 恢复该文件

## 二、git工作区与暂存区

### 1、工作区

​	就是电脑中自己创建的==仓库目录==

### 2、版本库

工作区中的==.git==隐藏目录，即为版本库，其中包含

- stage（暂存区）
- 自动创建的第一个分支master
- 以及指向master的指针HEAD

### 3、文件的转移

- 第一步：使用`git add` 添加文件，就是将工作区的文件添加至==.git==版本库中的暂存区
- 第二步：使用`git commit`就是将暂存区中的内容提交到当前分支上（master）

## 三、远程仓库 github仓库

### 1、创建SSH Key

执行`ssh-keygen -t rsa -C "sunyh0w0@163.com"`

生成公私秘钥对儿

### 2、登录github，设置SSH

在网站中找到setting设置，在左侧选择SSH，选择添加SSH Key

添加一个标题，key中存放公钥，最后点击保存

### 3、创建远程仓库

create  a new Repository

填写库名以及描述

### 4、将本地版本库中的内容同步 到远程仓库中

a)  执行`git remote add origin https://github.com/qiyuewu1/oneTest.git`

后边的链接标识新建的仓库地址，每个人的每个仓库都不同。

b)  推送至远程库`git push -u origin master`

- -u 表示第一次推送master分支时，会与远程仓库的master分支进行关联
- 以后推送就可以简化命令`git push origin master`

### 5、从远程仓库同步到本地

`git clone {仓库地址}`

## 四、分支

### 1、创建一个dev的分支

`git checkout -b dev`

- -b 表示创建并切换,表示如下两条命令
  - `git branch dev`
  - `git checkout dev`

### 2、查看当前分支

`git branch`

### 3、合并分支

a)  先试用切换分支`git checkout master`

b)  然后合并分支`git merge dev`==合并到当前分支==（上一步切换到的master）上

### 4、删除分支

a)  在合并完成后，可以将dev的分支删除 `git branch -d dev`

- -d 表示删除

### 5、解决冲突

<<< HEAD 表示最终合并到的文件，变动的内容，一般指master

\>>>分支名 表示分支提交的内容

### 6、隐藏工作现场，创建分支

`git stash`此时未提交的内容也不会显示在状态中

`git stash pop` 恢复现场

### 7、设置本地分支与远程分支建立连接

`git branch --set -upstream dev origin/dev

















