# git 基础知识

## 配置用户

1. 设置全局用户：

- git config --global user.name "用户名"
- git config --global user.email "邮箱"

2. 设置当地/项目用户：

- git config --local user.name "用户名"
- git config --local user.email "邮箱"

## 创建仓库

- git init 初始化仓库 在目录中执行 git init 就可以创建一个 Git 仓库了. 例如

1. mkdir tensorflow-practice
2. cd git
3. git init  
   现在你可以看到在你的项目中生成了 .git 这个子目录，这就是你的 Git 仓库了，所有有关你的此项目的快照数据都存放在这里

- git clone 拷贝一份远程仓库，也就是下载一个项目  
  命令格式如下： git clone [url]
  直接执行命令： git clone https://gitee.com/yangqiantao/tensorflow-practice.git


- [tensorflow-practice](https://gitee.com/yangqiantao/tensorflow-practice?_from=gitee_search) 项目是作者学习 tensorflow
  的记录，欢迎大家 STAR

## 提交与修改

Git 的工作就是创建和保存自己的项目快照及与之后的快照进行对比

### 　git add 添加文件到暂存区

1. 添加一个或多个文件到暂存区：git add [file1] [file2] ...
2. 添加指定目录到暂存区，包括子目录： git add [dir]
3. 添加当前目录下的所有文件到暂存区： git add .

### git status 查看仓库当前的状态，显示有变更的文件。

### git diff 比较文件的不同，即暂存区和工作区的差异。
git diff 命令显示已写入暂存区和已经被修改但尚未写入暂存区文件的区别。git diff 有两个主要的应用场景。
1. 尚未缓存的改动：git diff
2. 查看已缓存的改动： git diff --cached
3. 查看已缓存的与未缓存的所有改动：git diff HEAD
4. 显示摘要而非整个 diff：git diff --stat

git diff 查看差异  
- 显示暂存区和工作区的差异: git diff [file]  
- 显示暂存区和上一次提交(commit)的差异: git diff --cached [file] 或 git diff --staged [file]  
- 显示两次提交之间的差异: git diff [first-branch]...[second-branch]

### git commit 提交暂存区到本地仓库。

- 提交暂存区到本地仓库中: git commit -m [message] --->  [message] 可以是一些备注信息。  
- 提交暂存区的指定文件到仓库区： git commit [file1] [file2] ... -m [message]  
- -a 参数设置修改文件后不需要执行 git add 命令，直接来提交: git commit -a

### git reset 回退版本
命令 git reset [--soft | --mixed | --hard] [HEAD]

1. --mixed 为默认，可以不用带该参数，用于重置暂存区的文件与上一次的提交(commit)保持一致，工作区文件内容保持不变。
- 命令： git reset  [HEAD]
- git reset HEAD^ # 回退所有内容到上一个版本  
- git reset HEAD^ 修改的文件XXX # 回退 XXX 文件的版本到上一个版本  
- git reset 052e # 回退到指定版本 

2. --soft 参数用于回退到某个版本： 
- 命令：git reset --soft HEAD 
- 实例： git reset --soft HEAD~3  # 回退上上上一个版本 

3. --hard 参数撤销工作区中所有未提交的修改内容，将暂存区与工作区都回到上一次版本，并删除之前的所有信息提交
- 命令 git reset --hard HEAD 实例：  
- git reset –hard HEAD~3 # 回退上上上一个版本  
- git reset –hard bae128 # 回退到某个版本回退点之前的所有信息。   
- git reset --hard origin/master # 将本地的状态回退到和远程的一样

### git rm 删除工作区文件。

1. 删除本地文件 
- 将文件从暂存区和工作区中删除： git rm file   
  如果删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项 -f： git rm -f file

- 如果想把文件从暂存区域移除，但仍然希望保留在当前工作目录中，换句话说，仅是从跟踪清单中删除，使用 --cached 选项即可： git rm --cached file

- 文件从暂存区域移除，但工作区保留：git rm --cached xxx
- 可以递归删除，即如果后面跟的是一个目录做为参数，则会递归删除整个目录中的所有子目录和文件：git rm –r *

2. 删除远程文件  
暂无

### git mv 移动或重命名工作区文件。

### 分支管理

1. 创建分支 git branch testBranch
2. git checkout testBranch 创建分支testBranch
3. 切换分支 Switched to branch 'testBranch'
4. git checkout -b testBranch 创建并切换到分支，相当于 2 和 3 加起来
5. git branch 查看所有的分支信息 ，当前分支前带有*
6. git branch –all 查看所有的分支信息
7. git checkout master 切回主分支
8. git merge testBranch 合并 testBranch 分支 到主分支 master 上
9. git branch -d testBranch 删除 testBranch 本地分支
10. git push origin :testBranch 删除远程库上的分支
11. git push branch testBranch push本地分支testBranch到远程库
12. 推送分支 git push origin master 把该分支上的本地提交推送到远程库
13. git push origin branchName 推送其他分支

## 关联仓库
### 关联一个仓库

本地项目代码关联远程仓库并提交，命令如下：

1. git init
2. git remote add origin 项目地址
3. git pull origin master
4. git add .
5. git commit -am 'message'
6. git push origin master
7. git remote rm origin 移除远程库的关联；

### 关联两个仓库分别推送

- 方式一：定义不同的远程仓库名称，然后分别推送 多次推送，配了几个远程仓库就推送几次
- 方式二：在同一个远程仓库下添加另一个远程仓库的地址，然后推送 only一次推送

#### 方式一

1. 可以直接通过命令将 本地项目 和 gitee/GitHub 项目关联

- git remote add gitee gitee项目地址
- git remote add github github项目地址

2. 也可以通过修改本地项目的配置文件

- 首先，进入到项目的 .git 文件夹，打开 config 文件
- 然后，找到 [remote "origin"] ，复制一份remote到下面，修改 remote 的名字和 url 即可

> 例如  
> [core]  
> repositoryformatversion = 0   
> filemode = false   
> bare = false   
> logallrefupdates = true   
> symlinks = false   
> ignorecase = true
>
> [remote "gitee"]  
> url = https://gitee.com/yangqiantao/tensorflow-practice.git   
> fetch = +refs/heads/*:refs/remotes/origin/*
>
> [remote "github"]  
> url = https://github.com/NigeloYang/tensorflow-practice.git   
> fetch = +refs/heads/*:refs/remotes/origin/*
>
> [branch "master"]    
> remote = origin   
> merge = refs/heads/master

- 执行以下命令: git remote，可以看到配置的两个仓库
- 推送代码时，需要对两个仓库分别执行一次push命令，也就是多次推送

> 推送 git push gitee master  
> 获取 git pull gitee master  
> 推送 git push github master  
> 获取 git pull github master

#### 方式二

1. 通过命令将 gitee/github 项目地址添加到本地已有的remote下

- git remote set-url --add origin gitee/github项目地址

2. 也可以通过修改本地项目的配置文件

- 推送代码只需执行以下一条命令即可 git push

> 例如  
> [core]  
> repositoryformatversion = 0   
> filemode = false   
> bare = false   
> logallrefupdates = true   
> symlinks = false   
> ignorecase = true
>
> [remote "origin"]  
> url = https://gitee.com/yangqiantao/tensorflow-practice.git   
> url = https://github.com/NigeloYang/tensorflow-practice.git   
> fetch = +refs/heads/*:refs/remotes/origin/*
>
> [branch "master"]    
> remote = origin   
> merge = refs/heads/master
