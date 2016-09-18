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
__清除屏幕log信息 __
	
	clear
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
####Git使用说明
分布式代码管理工具。
# 
**配置Git命令快捷键**

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
**配置Git命令快捷键**
	
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

**git某个命令的帮助文档** 
	
	git --help 命令
	eg: git --help clone
	 
** 初次使用git拉取将仓库拉到本地 **
		
	进入项目根目录
	git status
	git clone git@IP：project
	eg: git clone git@192.168.1.22:evchargingposts/evcp-server.git
	
	以后 每次获取最新代码
	git pull （合并）or git fetch（不合并）
	
	将误删文件找回
	git checkout filename
** 初次取代码到本地仓库 **
	
	cd 项目目录
	git clone
	
** 初始使用 创建 .git 仓库 上传代码 **
	
	cd 代码所在路径/工作目录
	git init
	
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

### Docker 常用命令
1. 查看目前系统中已有的容器
2. 运行容器
	
	docker run －it 容器id
	eg: docker run -it gitlab/gitlab-ce
	
3. 运行已有的容器
	
	docker start 容器id
	
2. 停止容器
3. 
	
###brew - mac上的包管理器
类似于ubuntu下的apt－get
1. 安装包
	
	brew install xxxx
	eg: brew install git
	
2. 查看包
	
	brew search /正则表达式/
	eg: brew search /wget/
	
3. 列出已安装的包
	
	brew list
	
4. 更新 brew
	
	brew update
	
5. 显示软件信息
	
	brew info
	
6. 显示包依赖
	
	brew deps
	
###node js 测试项目
1.node的包管理器 － npm
主要功能，node包的安装，卸载，更新，查看，搜索，发布。

	1. 包安装 npm install ./ -g
	－全局安装：安装位置是./node_modules，package可以在所有的目录下使用。
	－本地安装：安装位置是/user/local，package只可以在当前安装目录下使用。
	查看所有安装的全局包 npm ls -g
	
	2. 卸载包 npm uninstall 包名
	3. 查看安装了哪些包 npm ls
	                 nmp ls －g
	4. 查看包信息 npm info 包名
	5. 更新包 npm update 包名
	    
2.node js 执行
	
	mocha nodejscode.js
		
**Sometimes I want a lot of text to be bold.
Like, seriously, a _LOT_ of text**

#### Blockquotes

> Right angle brackets &gt; are used for block quotes.

#### Links and Email

contact : email <gxl8483336@sohu.com>.

Simple inline link <http://chenluois.com>, another inline link [Smaller](http://25.io/smaller/), one more inline link with title [Resize](http://resizesafari.com "a Safari extension").

A [reference style][id] link. Input id, then anywhere in the doc, define the link with corresponding id:

[id]: http://25.io/mou/ "Markdown editor on Mac OS X"

Titles ( or called tool tips ) in the links are optional.

#### Images

An inline image ![Smaller icon](http://25.io/smaller/favicon.ico "Title here"), title is optional.

A ![Resize icon][2] reference style image.

[2]: http://resizesafari.com/favicon.ico "Title"

#### Inline code and Block code

Inline code are surround by `backtick` key. To create a block code:

	Indent each line by at least 1 tab, or 4 spaces.
    var Mou = exactlyTheAppIwant; 

####  Ordered Lists

Ordered lists are created using "1." + Space:

1. Ordered list item
2. Ordered list item
3. Ordered list item

#### Unordered Lists

Unordered list are created using "*" + Space:

* Unordered list item
* Unordered list item
* Unordered list item 

Or using "-" + Space:

- Unordered list item
- Unordered list item
- Unordered list item

#### Hard Linebreak

End a line with two or more spaces will create a hard linebreak, called `<br />` in HTML. ( Control + Return )  
Above line ended with 2 spaces.

#### Horizontal Rules

Three or more asterisks or dashes:

***

---

- - - -

#### Headers

Setext-style:

This is H1
==========

This is H2
----------

atx-style:

# This is H1
## This is H2
### This is H3
#### This is H4
##### This is H5
###### This is H6


### Extra Syntax

#### Footnotes

Footnotes work mostly like reference-style links. A footnote is made of two things: a marker in the text that will become a superscript number; a footnote definition that will be placed in a list of footnotes at the end of the document. A footnote looks like this:

That's some text with a footnote.[^1]

[^1]: And that's the footnote.


#### Strikethrough

Wrap with 2 tilde characters:

~~Strikethrough~~


#### Fenced Code Blocks

Start with a line containing 3 or more backticks, and ends with the first line with the same number of backticks:

```
Fenced code blocks are like Stardard Markdown’s regular code
blocks, except that they’re not indented and instead rely on
a start and end fence lines to delimit the code block.
```

#### Tables

A simple table looks like this:

First Header | Second Header | Third Header
------------ | ------------- | ------------
Content Cell | Content Cell  | Content Cell
Content Cell | Content Cell  | Content Cell

If you wish, you can add a leading and tailing pipe to each line of the table:

| First Header | Second Header | Third Header |
| ------------ | ------------- | ------------ |
| Content Cell | Content Cell  | Content Cell |
| Content Cell | Content Cell  | Content Cell |

Specify alignment for each column by adding colons to separator lines:

First Header | Second Header | Third Header
:----------- | :-----------: | -----------:
Left         | Center        | Right
Left         | Center        | Right


### Shortcuts

#### View

* Toggle live preview: Shift + Cmd + I
* Toggle Words Counter: Shift + Cmd + W
* Toggle Transparent: Shift + Cmd + T
* Toggle Floating: Shift + Cmd + F
* Left/Right = 1/1: Cmd + 0
* Left/Right = 3/1: Cmd + +
* Left/Right = 1/3: Cmd + -
* Toggle Writing orientation: Cmd + L
* Toggle fullscreen: Control + Cmd + F

#### Actions

* Copy HTML: Option + Cmd + C
* Strong: Select text, Cmd + B
* Emphasize: Select text, Cmd + I
* Inline Code: Select text, Cmd + K
* Strikethrough: Select text, Cmd + U
* Link: Select text, Control + Shift + L
* Image: Select text, Control + Shift + I
* Select Word: Control + Option + W
* Select Line: Shift + Cmd + L
* Select All: Cmd + A
* Deselect All: Cmd + D
* Convert to Uppercase: Select text, Control + U
* Convert to Lowercase: Select text, Control + Shift + U
* Convert to Titlecase: Select text, Control + Option + U
* Convert to List: Select lines, Control + L
* Convert to Blockquote: Select lines, Control + Q
* Convert to H1: Cmd + 1
* Convert to H2: Cmd + 2
* Convert to H3: Cmd + 3
* Convert to H4: Cmd + 4
* Convert to H5: Cmd + 5
* Convert to H6: Cmd + 6
* Convert Spaces to Tabs: Control + [
* Convert Tabs to Spaces: Control + ]
* Insert Current Date: Control + Shift + 1
* Insert Current Time: Control + Shift + 2
* Insert entity <: Control + Shift + ,
* Insert entity >: Control + Shift + .
* Insert entity &: Control + Shift + 7
* Insert entity Space: Control + Shift + Space
* Insert Scriptogr.am Header: Control + Shift + G
* Shift Line Left: Select lines, Cmd + [
* Shift Line Right: Select lines, Cmd + ]
* New Line: Cmd + Return
* Comment: Cmd + /
* Hard Linebreak: Control + Return

#### Edit

* Auto complete current word: Esc
* Find: Cmd + F
* Close find bar: Esc

#### Post

* Post on Scriptogr.am: Control + Shift + S
* Post on Tumblr: Control + Shift + T

#### Export

* Export HTML: Option + Cmd + E
* Export PDF:  Option + Cmd + P


### And more?

Don't forget to check Preferences, lots of useful options are there.

Follow [@Mou](https://twitter.com/mou) on Twitter for the latest news.

For feedback, use the menu `Help` - `Send Feedback`