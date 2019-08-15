 [来自官方教程](https://git-scm.com/docs "With a Title"). 

## 基本概念
### Git中文件有三种状态：

+ 已修改（modified）
+ 已暂存（staged）
+ 已提交（committed）

### Git 项目的三个工作区域：

工作目录、暂存区域、Git 仓库（本地仓库/远程仓库）
<img src="github.png" style="zoom:30%" >

### 第一次上传 Github 的流程如下：
1. 将文件加入追踪并放到stage区域：git add
2. 提交更新：找到暂存区域的文件，将暂存区域永久性存储到本地Git仓库的master分支：git commit
3. 上传服务器，将本地master上传到GitHub/远程服务器:git push

### 更新版本后上传Github流程如下：

1. 在工作目录中修改文件。
2. 将修改的文件放入暂存区:git add
3. 提交更新：找到暂存区域的文件，将暂存区域永久性存储到本地Git的分支：git commit
4. 上传服务器，将本地分支上传到GitHub/远程服务器:git push


## 详细操作
#### 创建仓库

    git init #创建本地git仓库

#### 将文件加入追踪方法1：正向添加
    
    git add toy/*.py #添加文件到track,以后git会追踪你的modify
    git add ./*.py
    git add ./*.sh
    git add readme.md

评价：优点：操作简单。缺点：在后面git status 会一直提示untracked file

#### 将文件加入追踪方法2：反向添加（推荐）

创建.gitignore文件 ：Specifies intentionally untracked files to ignore
并自定义需要忽略的文件

        git add . #添加除了被忽略的之外的所有文件

评价：缺点：需要了解.gitignore文件的规则。优点：在后面git status会忽略被忽略的文件的状态

#### 列出目前所有被追踪的文件

    git ls-tree -r master --name-only

### 你目前所需要知道的
----

#### 将修改的文件放入暂存区

    git add -u #将已追踪的修改文件放入暂存区
    git add . #将所有的文件放入暂存区，包括没有追踪的，不包括gitignore的
  
    git status #查看哪些文件处于什么状态：changes not staged for commit(修改但没有放入暂存区)changes to be committed（放入暂存区将要提交）
    git diff #具体查看文件哪里修改(enter下一行 q退出)

目前为止，暂存区域已经准备妥当可以提交了。 在此之前，请一定要确认还有什么修改过的或新建的文件还没有git add 过，否则提交的时候不会记录这些还没暂存（changes not staged for commit）起来的变化。  

所以准备提交前，可以先用 git status 看下，是不是都已暂存起来了（changes to be committed）， 然后再运行提交命令。


#### 提交到本地分支

    git commit -m "your commit message e.g.fixed some bugs"
    git commit --amend  #想追加注释，ctrl+o 保存 ctrl+x 退出
    git reset --soft HEAD^ #如果后悔了，执行完commit后，想不删除工作空间改动代码，撤销commit，并且撤销git add
    git show-branch -a #可视化所有提交的版本

#### 将本地分支上传到github

    git push http://github.com/xxx/hello.git #上传github
    git push -u origin master -f #如果报错强制push
    git remote set-url origin http://github.com/GarfieldF/RGBT-tracking.git #如果地址错误，重定向GitHub仓库地址

----
### 团队协作
    git pull #拉取远端仓库= git fetch git merge #获取你的小伙伴上传的分支，和你的分支合并，如果有冲突手动选择保留哪个版本

    git slash #会把所有未提交的修改（包括暂存的和非暂存的）都保存起来，用于后续恢复当前工作目录。
    #等到修完Bug，提交到服务器上后，再使用git stash apply将以前的工作恢复回来。

----
## 其他
###　Connecting to GitHub with SSH
作用：一劳永逸的配置，不再需要每次上传本地仓库都登陆github。

 [可以直接按照官网教程配置](https://help.github.com/en/articles/connecting-to-github-with-ssh "With a Title"). 

１．配置名称和邮箱

    git config --global user.name "GarfieldF"
    git config --global user.email "xxx@163.com"
  
生成新的密钥

    ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
    
添加到你的github账号设置中
GitHub网站  -- 点击右上角你的头像 settings  --  SSH and GPG keys --New SSH key
将你的密钥加进去
以后就不需要登陆了


### 从GitHub克隆仓库

    git clone http://github.com/GarfieldF/RGBT-tracking
  
### 从GitHub下载并添加子模块

    git submodule add http://
  
