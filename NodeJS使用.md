
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
		