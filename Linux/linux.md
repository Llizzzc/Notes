# Linux
>1. [尚硅谷](https://www.bilibili.com/video/BV1dW411M7xL?p=9 "linux")
>2. [菜鸟教程](https://www.runoob.com/linux/linux-tutorial.html "linux")
>3. [查命令](https://wangchujiang.com/linux-command/ "linux")

## 一、网络连接
1. 桥连接：Linux可以和其他系统通信，但是可能导致ip冲突
2. NAT(常用)：Linux可以通过主机ip转换来访问外网，不会造成ip冲突
	+ `ping Ip`	// 测试主机之间网络连通性
	+ `ifconfig`	// 查看ip和网关
3. 主机模式：Linux是独立主机，不能访问外网

## 二、系统分区
必须的分区：/、/boot(200MB)、swap(交换分区，一般是分配物理内存的1.5~2倍)
+ `lsblk (-f)`	// 查看所有设备挂载情况

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
+ `ssh -p Port UserName@Ip`	// 连接服务器，-p为端口，22端口
+ `exit`	// 退出服务器
+ `ssh-keygen -R Ip`	// 删除远端密钥
+ `scp -P Port (-r) UserName@Ip:绝对路径 本地绝对路径`	// 下载，-r代表文件夹
+ `scp -P Port (-r) 本地绝对路径 UserName@Ip:绝对路径`	// 上传
+ `sftp -P Port UserName@Ip`	// 建立sftp传输连接，cd代表远程操作，lcd代表本地操作
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
	+ `/KeyWord`	// 查找，按n查找下一个
	+ `set nu`	// ==命令行下==，设置文件行号
	+ `set nonu`	// 取消行号
	+  `G`	// 到文档末尾
	+  `gg`	// 回到开头
	+  `u`	// 撤销
	+  `(n)shift + g`	// 先显示行号，n代表移动到第n行
	+  `(n)space`	// 向右移动这一行n个字符
	+  `0`	// 数字0，移动到这一行最前
	+  `$`	// 移动到这一行最后
	+  `ctrl + (f b)`	// f下翻，b上翻
	+  `.`	// 重复上一个动作

## 六、用户管理
用户至少要属于一个组，家目录为/home，用户登录时自动进入家目录
1. 关机重启
	+ `shutdown (-h -r) (now 1)`	// -h关机，-r重启，now为立刻，1表示一分钟后关机
	+ `halt`	// 关机
	+ `reboot`	// 重启
	+ `sync`	// 保存数据，关机前执行一下
2. 登录注销
	+ `logout`	// 注销，图形界面注销无效
3. 用户
	+ `useradd (-d DirectoryName -g GroupName -m -s) UserName`	// 创建用户，同时创建与用户同名的组和家目录，-d表示指定家目录，-m表示不存在家目录则创建，-g指定组，-s为登陆shell
	+ `passwd UserName`	// 改密
	+ `userdel (-r) UserName`	// 删除用户，-r表示同时删除家目录
	+ `usermod -g GroupName UserName`	// 修改用户属组
4. 查询切换用户
	+ `id UserName`	// 查询信息
	+ `su - UserName`	// 切换用户，权限高切到低不需要密码，exit回到之前用户
	+ `whoami`	// 查看当前用户
5. 用户组
	+ `groupadd GroupName`	// 创建组
	+ `groupdel GroupName`	// 删除组
6. 权限管理
	d(目录)、l(链接文件)、-(普通文件)、r=4、w=2、x=1
	![](./img/01.jpeg)
	+ `chown (-R) UserName(:GroupName) FileName`	// 更改文件目录所有者，也可以改所在组，-R表示递归更改
	+ `chgrp (-R) GroupName FileName`	// 更改文件目录所在组
	+ `chmod u=(rwx),g=(rwx),(o=rwx),(a=rwx) FileName`	// 更改文件目录权限，u为所有者，g为所在组，o为其他人，a=u+g+o为所有人
7. 用户和组相关文件
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
1. 帮助
	+ `init n`	// 更改运行级别
	+ `man Command`	// 查询命令
	+ `help Command`	// 只能查询内置命令
2. 文件目录
	+ `pwd`	// 显示当前工作目录绝对路径
	+ `ls (-a -l -h) (DirectoryName)`	// 列出目录下文件，-a包括隐藏文件，-l包括文件权限，-h显示计量单位
	+ `cd DirectoryName(. .. ~)`	// .为当前目录，..为上一级，~为家目录，可以使用绝对路径
	+ `mkdir (-p) DirectoryNmae`	// 创建目录，-p为一次创建多级目录
	+ `rmdir (-p) DirectoryNmae`	// 删除空目录 ，-p为删除该目录后，若上一级变为空目录则也删除
	+ `touch FileName1 FileName2`	// 创建文件
	+ `cp (-r -i) Source Destination`	// 复制文件，-r为递归复制整个目录，-i为覆盖前询问
	+ `rm (-r -f) (DirectoryName FileName)`	// 删除文件或目录，-r递归删除，-f强制不提示
	+ `mv Source Destination`	// 移动文件或目录，也可以重命名
	+ `cat (-n) FileName`	// 查看文件，只读，-n显示行号
	+ `more FileName`	// 查看文件，一页一页显示
	+ `less FileName`	// 看大文件方便
	+ `(echo Context cat FileName ls -l) (> >>) FileName`	// 将指定内容写入文件，>为覆盖，>>为追加
	+ `echo Context`	// 输出内容到控制台
	+ `head (-n Num) FileName`	// 显示文件前10行，-n指定行数
	+ `tail (-n Num -f) FileName`	// 显示文件最后10行，-f实时追踪更新
	+ `ln (-s) Source LinkName`	// 给原文件创建软链接，指向原文件，-s表示可以为目录
	+ `history (n)`	// 显示历史指令，n指定最近n条指令
3. 时间日期
	+ `date (-s) ("+%y-%m-%d %H:%M:%S")`	// 显示当前时间，可以指定格式，-s为设置时间
	+ `cal (Year)`	// 显示日历，可以显示指定年份下所有
4. 搜索查找
	+ `find DirectoryName (-name FileName -user UserName -size (+ -)n)`	// 在指定目录下查找，按名称，所有者，大小查找，+为大于，-为小于
	+ `locate FileName`	// 先执行updatedb，再查找
	+ `grep (-n -i) KeyWord FileName`	// 关键字查找，-n显示行号，-i不区分大小写，|管道符号，将前一个指令结果传给下一个指令
5. 压缩和解压
	+ `gzip FileName`	// 压缩，不保留原先文件
	+ `gunzip FileName.gz`	// 解压
	+ `zip (-r) FileName.zip FileName`	// -r压缩整个目录
	+ `unzip (-d DirectoryName) FileName.zip`	// -d指定解压路径
	+ `tar -cvzf FileName.tar.gz DirectoryName`	// 可以为单独文件，-c产生.tar文件，-v显示详细信息，-f指定压缩后的文件名，-z打包
	+ `tar -xvzf FileName.tar.gz (-C DirectoryName)`	// -x解压，-C指定目录，必须存在该目录
6. 任务调度
	+ `crontab -e(-r -l)`	// 执行后编辑，开头五个占位符(分钟0-59)(小时0-23)(日期1-31)(月1-12)(星期0-7，0和7都代表周日)，\*表示任何时间，，表示不连续时间，-表示连续时间，\*/n代表时间间隔，紧接脚本路径或指令，保存后退出，-r终止，-l列出当前任务调度
	+ `service crond restart`	// 重启任务调度
7. 磁盘管理
	+ `df (-l -h)`	// 查看系统磁盘使用情况，-h带计量单位，-l表示本地
	+ `du (-h -a -c --max-depth=) DirectoryName`	// 查看指定目录磁盘情况，-a代表包括文件，--max-depth指定查询深度，-c列出明细同时增加汇总
	+ `tree DirectoryName`	// 将目录按树形表示
8. 进程管理
	+ `ps (-aux -ef)`	// 查看系统执行的进程，-e显示所有进程，-f包括父进程，-a显示当前终端所有进程，-u以用户格式显示，-x显示后台运行参数
	+ `top (-d -i -p)`	// 动态监控进程，-d指定更新间隔，-p监控指定进程，-i不显示闲置和僵尸进程，可以输入u指定显示某个用户的进程，k终止某个进程
	+ `pstree (-u -p)`	// 树状显示，-p显示pid，-u显示所属用户
	+ `netstat (-anp)`	// 查看网络情况，-an指按一定顺序输出，-p显示哪个进程在调用
	+ `kill (-9) Pid`	// 终止进程，-9强制
	+ `killall ProcessName`	// 通过名字终止进程
9. 服务管理，/etc/init.d
	+ `service ServerName (start stop restart reload status)`	// 服务指令
	+ `telnet Ip Port`	// 检查linux某个端口是否在监听，并可以访问
	+	`chkconfig (--Level n) (ServerName) (on off) (--list)`	// 显示或设置每个服务的各个运行级别状态

## 八、包管理
1. ubuntu，/etc/apt/sources.list默认为官方软件库，备份后更换为国内源，默认不支持远程登录
  + `apt-get update`	// 更新源
  + `apt-get install Package (--reinstall)`	// 安装包，可重装
  + `apt-get remove Package (--purge)`	// 删除包，可选清除配置文件
  + `apt-cache search Package`	// 搜索包
  + `apt-cache show Package`	// 获取包相关信息
  + `apt-get upgrade`	// 更新已安装的包
  + `apt-get autoclean`	// 删除过期的包
  + `apt list --installed`	// 查看已安装的包
  + `apt-get source Package`	// 下载包源代码 
  + `apt-get -f install`	// 修复安装
  + `apt-get install openssh-server`	// 安装sshd服务
  + `service sshd start`	// 启动sshd服务
2. centos，/etc/yum.repos.d/CentOS-Base.repo，备份后换为国内源
	+ `yum install Package`	// 下载包
	+ `yum list | grep Package`	// 查找包
	+ `yum update Package`	// 更新所有需要更新的包
	+ `yum check-update`	// 检查系统中需要更新的包
	+ `yum list installed`	// 显示已安装的包
	+ `yum info Package`	// 显示包信息
	+ `yum remove Package`	// 删除包
	+ `yum clean`	// 清除缓存文件