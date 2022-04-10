# Linux
>1. [尚硅谷](https://www.bilibili.com/video/BV1dW411M7xL?p=9 "linux")
>2. [菜鸟教程](https://www.runoob.com/linux/linux-tutorial.html "linux")
>3. [查命令](https://wangchujiang.com/linux-command/ "linux")

## 一、网络连接
1. 桥连接：Linux可以和其他系统通信，但是可能导致ip冲突
2. NAT（常用）：Linux可以通过主机ip转换来访问外网，不会造成ip冲突
3. 主机模式：Linux是独立主机，不能访问外网

## 二、系统分区
必须的分区：/、/boot(200MB)、swap(交换分区，一般是分配物理内存的1.5~2倍)

## 三、目录结构
|<span style="color:red">/bin; /usr/bin; /usr/local/bin</span>|/sbin; /usr/sbin; /usr/local/sbin|<span style="color:red">/home</span>|<span style="color:red">/root</span>|
|:--|--|--|--|
|常用命令|系统管理员使用命令|普通用户主目录|系统管理员|
|**/lib**|**/lost+found**|<span style="color:red">**/etc**</span>|<span style="color:red">**/usr**</span>|
|开机所需最基本的动态连接共享库|系统非法关机后会存放一些文件|所有的系统管理所需的配置文件|用户的很多应用和文件|
|<span style="color:red">**/boot**</span>|**/proc**|**/srv**|**/sys**|
|启动核心文件|内核|内核|内核|
|**/tmp**|**/dev**|<span style="color:red">**/media**</span>|<span style="color:red">**/mnt**</span>|
|临时文件|把所有硬件用文件形式存储|设备如U盘、光驱等|识别别的文件系统|
|**/opt**|<span style="color:red">**/usr/local**</span>|<span style="color:red">**/var**</span>|**/selinux**|
|安装包|安装完的软件|不断变化的文件，包括日志|安全子系统|

## 四、远程连接
+ `ssh -p Port User@Host`	// 连接服务器
+ `exit`	// 退出服务器
+ `scp -P Port (-r) User@Host:绝对路径 本地绝对路径`	// 下载，-r代表文件夹，22端口
+ `scp -P Port (-r) 本地绝对路径 User@Host:绝对路径`	// 上传
+ `sftp -P Port User@Host`	// 建立sftp传输连接，cd代表远程操作，lcd代表本地操作
+ `get (-r) 远程路径 本地路径`	// 下载
+ `put (-r) 本地路径 远程路径`	// 上传

## 五、编辑器
1. 三种模式：
	+ 正常模式：打开即正常模式，可以使用快捷键
	+ 编辑模式：输入内容，按i、a、o、r等进入
	+ 命令行模式：完成读取、保存、离开等操作，先esc进入正常模式，按:进入，q!强制退出
2. 常用快捷键：
	+ `(n)yy`	// 复制当前行，n表示从当前行开始往下一共复制n行，p粘贴
	+ `(n)dd`	// 删除，同复制
	+ `/KeyWord`	// 查找，输入n查找下一个
	+ `set nu`	// ==命令行下==，设置文件行号
	+ `set nonu`	// 取消行号
	+  `G`	// 到文档末尾
	+  `gg`	// 回到开头
	+  `u`	// 撤销
	+  `(n)shift + g`	// 先显示行号，n代表移动到第n行
	+  `(n)space`	// 向右移动这一行n个字符
	+  `0`	// 数字0，移动到这一行最前
	+  `$`	// 移动到这一行最后
	+  `ctrl + f`	// 下翻
	+  `ctrl + b`	// 上翻
	+  `.`	// 重复上一个动作

## 六、用户管理
用户至少要属于一个组，家目录为/home，用户登录时自动进入家目录
1. 关机重启
	+ `shutdown -h now(1)`	// 立即关机，1表示一分钟后关机
	+ `shutdown -r now`	// 立即重启
	+ `halt`	// 关机
	+ `reboot`	// 重启
	+ `sync`	// 保存数据，关机前执行一下
2. 登录注销
	+ `logout`	// 注销，图形界面注销无效
3. 用户
	+ `useradd (-d UserDirectory) (-g GroupName) (-m) UserName`	// 创建用户，同时创建与用户同名的组和家目录，-d表示指定家目录，-m表示不存在该目录则创建，-g指定组
	+ `passwd UserName`	// 改密
	+ `userdel (-r) UserName`	// 删除用户，-r表示同时删除家目录
	+ `usermod -g GroupName UserName`	// 修改属组
4. 查询切换用户
	+ `id UserName`	// 查询信息
	+ `su - UserName`	// 切换用户，权限高切到低不需要密码，exit回到之前用户
	+ `whoami`	// 查看当前用户
5. 用户组
	+ `groupadd GroupName`	// 创建组
	+ `groupdel GroupName`	// 删除组
6. 用户和组相关文件
	+ 用户配置文件：/etc/passwd，用户名：口令：用户标识：组标识：注释描述：家目录：登录shell
	+ 组配置文件：/etc/group，组名：口令：组标识：组内用户
	+ 口令配置文件：/etc/shadow，登录名：加密口令：最后一次修改时间：最小时间间隔：最大时间间隔：警告时间：不活动时间：失效时间：标志

## 七、实用指令
|0|1|2|3|
|--|--|--|--|
|关机|单用户找回秘密|多用户无网络服务|多用户有网络服务|
|**4**|**5**|**6**|**运行级别（/etc/inittab）**|
|系统未使用|图形界面|系统重启|3，5使用多|

root找回密码：启动时按enter，按e，选中内核再按e，输入空格1回车，然后输入b启动改密码
+ `init Num`	// 更改运行级别

