# Mou

![Mou icon](http://25.io/mou/Mou_128.png)

## Overview

**Linux**,  *常用命令* ，常用*开发工具*等，使用手记.

### Linux

#### 系统命令

**提升用户权限（change root 切换用户)**

	su
	
**临时提升权限(change root)**

	sudo
**创建文件**
	
	touch xxxx.xxx

__创建目录__ 
	
	mkdir  xxx

**删除文件 **
	
	rm -r 文件夹
__强制删除 不询问__
	
	 rm -f  文件或文件夹
** 退到上一次打开的目录 **
	
	cd - 

** 回到用户主目录 **

	
	cd           #回到主目录
    cd ~         #同样也是回到主目录
** 当前用户的根目录 ～ **
** 当前目录 . **
    
__清除屏幕log信息 __
	
	clear
	Mac 中 快捷键 command+k
	
** 将文件内容考入剪切板 **
	
	pbcopy <  文件名 
	eg: pbcopy < ~/.ssh/id_rsa.pub
__修改文件权限 __
	
	chmod 777 文件名
	
** 查询命令使用说明 **
	
	man 命令 
	命令 --help
**查看文件内容（只读）**
	
	cat 文件名
**打开文件或者目录 **
	
	open 文件或者目录
	eg 打开上两层目录 open ../../doc/api


_配合 tap 快捷键，随时可以查看指定目录中的文件有哪些_

__编辑文件 __
	
	vi 文件名
	vim 文件

** 域名解析查询 dig **

	dig www.baidu.com
	类似命令 nslookup
	
** 只读文件的修改 **

	su
	chmod 777 /etc/profile
	wq!
** 查看 文件权限 **
   ls -l
** 查看隐藏文件 **
   ls -a
** source命令：** 
source命令也称为“点命令”，也就是一个点符号（.）。source命令通常用于重新执行刚修改的初始化文件，使之立即生效，而不必注销并重新登录。
用法： 
	source filename 
    . filename
    
** grep **
  
** more **

** top **