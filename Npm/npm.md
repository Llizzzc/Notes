# Npm
>1. [Npm命令](https://blog.csdn.net/u012982629/article/details/80676928?spm=1001.2101.3001.6650.14&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-14.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-14.pc_relevant_default&utm_relevant_index=18)

## 常用命令
+ 项目上传github时要忽略node_modules目录
+ 所有模块包必须以单独目录存在，其顶级目录下需要包含package.json文件，该文件必须包含name、version、main(模块入口)三个属性
+ 模块在第一次加载会被缓存，内置模块加载优先级最高
+ 导入自定义模块时省略拓展名，则会自动尝试补全js、json、node拓展名，否则报错
+ 第三方模块加载，先在当前目录下查找，否则移动到上层目录查找，直到根目录
+ 目录作为模块标识符，先在当前目录查找package.json文件的main属性，否则加载目录下的index.js文件，没有则报错
+ `npm list`	// 查看当前目录已安装模块
+ `npm list -g`	// 查看全局模块
+ `npm init -y`	// 初始化项目会出现一个package.json的配置文件，-y为快速，只能英文目录，不能包含空格
+ `npm update PackageName`	// 更新指定模块
+ `npm config list`	// 查看配置信息
+ `npm list PackgeName`	// 查看当前目录模块版本
+ `npm info PackageName`	// 查看当前目录模块的详细信息，包括各版本号等
+ `npm view PackageName version`	// 查看模块远程最新版本
+ `npm view PackageName versions`	// 查看模块远程所有版本
+ `npm install PackageName` // 当前目录安装模块
+ `npm install`	// 会读取package.json的依赖，自动安装所有模块
+ `npm install PackageName@Version`	// 安装模块的指定版本
+ `npm install PackageName -g`	// 系统全局安装模块
+ `npm install PackageName --save`	// 安装好后写入package.json的dependencies中(开发上线都用得到的环境依赖)
+ `npm install PackageName --save-dev`	// 安装好后写入package.json的devDepencies中(只有开发用得到的环境依赖)
+ `npm uninstall PackageName`	// 删除当前目录模块
+ `npm uninstall PackageName -g`	// 卸载系统全局模块
+ `npm uninstall PackageName --save`	// 删除模块，同时删除模块留在package.json中dependencies下的对应信息
+ `npm uninstall PackageName --save-dev`	// 删除模块，同时删除模块留在package.json中devDependencies下的对应信
+ `nrm ls`	// 查看所有源
+ `nrm use Name`	// 切换源	
+ `nrm test Name`	// 源测速
+ `npm login`	// 终端登录，需要将源换为官方源发布
+ 发布包起码需要包含js文件、README.md、package.json，其中json中包含name、version、main、description(描述功能)、keywords(便于用户检索)、license(一般为ISC)属性
+ `npm publish`	// 发布包
+ `npm unpublish PackageName --force`	// 只能删除72小时内发布的包，删除的包24小时内不允许重复发布