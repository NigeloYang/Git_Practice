# git 基础知识

## 配置用户

1. 设置全局用户：  
- git config --global user.name "用户名"
- git config --global user.email "邮箱"

2. 设置当地/项目用户：
- git config --local user.name "用户名"
- git config --local user.email "邮箱"

## 创建仓库

## 基本操作说明

1. git init 初始化一个git 仓库；
2. git add test.txt 添加一个文件到仓库，可以添加多个，一空格隔开；或者直接添加所有的： git add .
3. git commit -m “remarks” 把文件提交到仓库；
4. git status 当前仓库的状态，哪些修改了，哪些还未提交等；
5. git remote 查看远程库的信息
6. git remote -v 查看上传协议 SSH/HTTPS
7. git remote
8. 同步与改动

> - git fetch origin
> - git reset --hard origin/master 丢弃在本地的所有改动与提交，重新从服务器获取最新的版本历史，并将本地主分支指向它；
> - git checkout --<filename>    若操作失误，替换掉本地改动，添加到暂缓区的文件不受影响；

9. git reset --hard HEAD^ 把当前版本回退到上一个版本；

10. 删除 rm <file>    删除本地的文件，若删错了，可以用checkout指令； git rm <file>    删除版本库的文件，删掉后commit提交；

11. git push -u origin master 把本地库的当前内容推送到远程库，参数-u是把本地主分支和远程主分支关联起来；

12. 关联与取消 git remote add origin git@github.com:xxxxxxx.git 关联一个远程库； git remote rm origin 移除远程库的关联；

9. git reset --hard HEAD^ 把当前版本回退到上一个版本；

10. 删除

    rm <file>    删除本地的文件，若删错了，可以用checkout指令； git rm <file>    删除版本库的文件，删掉后commit提交；


11. git push -u origin master

把本地库的当前内容推送到远程库，参数-u是把本地主分支和远程主分支关联起来；

12. 关联与取消

    git remote add 项目名 项目地址 关联一个远程库； git remote rm origin 移除远程库的关联；

### 分支管理

1. 分支 git branch testBranch 
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


15. 更新当前分支 git pull

16. 本地提交 git commit -am 当你本地的文件都已经用git add “” 或之前已经添加到缓存区后，这时本地文件有所改动(修改过的或新加入的)，需要进行commit 提交，使用git commit -am
    “remark”即可全部提交到staged，最后 git push到远程库；
    ***注意：在分支切换之前最好先commit全部的改变，除非你真的知道自己在做什么!


17. 添加所有的 git add -A 不再需要一个个的单独添加

18. 追踪未添加的文件git add . git add . //不但可以跟单一文件，还可以跟通配符，更可以跟目录。一个点就把当前目录下所有未追踪的文件全部add了

19. git reset HEAD a.txt 撤销暂存的文件 （已经添加到暂存区了）

21.常用操作命令
5.回退到指定版本 git reset –hard 提交记录id

## 关联仓库
### 关联一个仓库
本地项目代码关联远程仓库并提交，命令如下：
  1. git init
  2. git remote add origin 项目地址
  3. git pull origin master
  4. git add .
  5. git commit -am 'message'
  6. git push origin master

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
> url = gitee项目地址   
> fetch = +refs/heads/*:refs/remotes/origin/*  
> 
> [remote "github"]  
> url = github项目地址   
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

####　方式二
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
> url = gitee项目地址   
> url = github项目地址   
> fetch = +refs/heads/*:refs/remotes/origin/*
> 
> [branch "master"]    
> remote = origin   
> merge = refs/heads/master
