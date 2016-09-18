# Git

## Overview

####Git使用说明
参考  link http://www.cnblogs.com/angeldevil/p/3238470.html
分布式代码管理工具。
记录版本信息的方式主要有两种：
 － 记录文件每个版本的快照
 － 记录文件每个版本之间的差异
　　GIT采用第一种方式。像Subversion和Perforce等版本控制系统都是记录文件每个版本之间的差异，这就需要对比文件两版本之间的具体差异，但是GIT不关心文件两个版本之间的具体差别，而是关心文件的整体是否有改变，若文件被改变，在添加提交时就生成文件新版本的快照，而判断文件整体是否改变的方法就是用SHA-1算法计算文件的校验和。
　　
　　GIT仓库所在的目录称为工作目录，
　　
　　　在工作目录中的文件被分为两种状态，一种是已跟踪状态(tracked)，另一种是未跟踪状态(untracked)。只有处于已跟踪状态的文件才被纳入GIT的版本控制。
　　　
　　　当我们往工作目录添加一个文件的时候，这个文件默认是未跟踪状态的，我们肯定不希望编译生成的一大堆临时文件默认被跟踪还要我们每次手动将这些文件清除出去。用以下命令可以跟踪文件：
　　　git add filename
# 
**1. 配置Git命令快捷键**

	vi ~/.gitconfig
	添加下述内容
	[alias]
    co = checkout
    ci = commit
    st = status
    pl = pull
    ps = push
    dt = difftool
    l = log --stat
    cp = cherry-pick
    ca = commit -a
    b = branch
**2. 配置Git命令快捷键**
	
	vi ~/.gitconfig
	添加下述内容
	[user]
        email = gxl8483336@sohu.com
        name = gxl8483336@sohu.com
    等价于
    git config --global user.name 
    git config --global user.email
    eg: git config --global "gxl8483336@sohu.com"
    git config --global gxl8483336@sohu.com 

**3. git某个命令的帮助文档** 
	
	git --help 命令
	eg: git --help clone
	
** 4. 初始使用 创建 .git 仓库 上传代码 **
	
	cd 代码所在路径/工作目录
	git init
	可以看到，多了个.git,关于git的所有版本信息等，均在此目录下。
	 
**5. 克隆一份远程的完全镜像到本地 － 初次使用git拉取将仓库拉到本地 **
		
	进入Git要管理的项目根目录，
	git status
	git clone git@IP：project
	eg: git clone git@192.168.1.22:evchargingposts/evcp-server.git
	克隆远程目录，由于是将远程服务器上的仓库完全镜像一份至本地，而不是取某一个特定版本，所以用clone而不是checkout
	
	以后 每次获取最新代码
	git pull （合并）or git fetch（不合并）
	
	将误删文件找回
	git checkout filename
** 初次取代码到本地仓库 **
	
	cd 项目目录
	git clone
	

	
** 从远程获取代码的新版本 不合并 **
	
	git fetch
	
** 从远程获取最新代码 并与本地代码 合并 **
	
	git pull

** 修改代码后 提交代码到本地仓库 **
	
	git add filename // 如果是新加的文件，需要add
	git commit filename // 提交索引的文件
	
** 修改代码后 提交代码到远程仓库 **
	
	git push
	
** 当想恢复某个被修改的文件 **
	
	cp A_from B_to
	git checkout A
