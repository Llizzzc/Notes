# Linux
>

## 文件结构
**重要文件**：**/etc**(系统配置文件)；**/bin**(用户使用指令)；**/usr/bin**(同上)；**/sbin**(root使用指令)；**/usr/sbin**(同上) ；**/var/log**(每个程序产生的日志)；**./**(当前目录)；**../**(上层目录)；**.**(表示隐藏目录或者文件)；**～**(用户目录)

## 文件基本属性
**文件属性以及文件所属用户和组，各位置代表内容如下**：

![users](./img/01.jpeg)

File type（**d**：目录；**-**：文件；**l**：软链接文档）

Permissions（**r**：读；**w**：写；**x**：执行；**-**：无权限）

**更改文件或目录属主&属组**：chown [-**R**：该目录下所有] owner file；chown [-**R**] owner:group file

**更改文件或目录属组**：chgrp [-**R**] group file

**更改文件或目录属性**：（**r**：4；**w**：2；**x**：1；**u**：user；**g**：group；**o**：others；**a**：all）chmod [-**R**] r+w+x file；chmod [-**R**] u+r,g+r,o+r file

## 文件与目录管理
**列出目录**：ls [-**a**：所有；**d**：目录本身；**l**：包含属性] dic

**切换目录**：cd 相对路径或绝对路径

**显示路径**：pwd [-**P**：确实路径，而非link file]

**创建目录**：mkdir [-**m**：配置文件属性；**p**：创建多个目录] dic

**删除空目录**：rmdir [-**p**：连同上级空目录一起] dic

**复制文件或目录**：cp [-**i**：目的地存在则询问是否覆盖；**r**：递归复制；**p**：连同文件属性一起复制；**d**：来源为link file则复制该属性；**a**=pdr] source destination

**移除文件或目录**：rm [-**f**：强制；**i**：移除前询问；**r**：递归删除] dic/file

**移动或者重命名文件或目录**：mv [-**f**：强制；**i**：询问；**u**：已存在则来源更新才覆盖] source destination

**由第一行显示文件内容**：cat -[-**b**：显示行号，仅对非空行；**E**：显示结尾$；**n**：显示行号，包括空行；**T**：将tab键以^I 显示；**v**：列出一些看不出的字符；**A**=vET] file

**倒着显示文件**：tac file

**一页一页翻动**：more file（**space**：下一页；**enter**：下一行；**b**：上一页；**q**：离开）；less file（**space**：下一页；**pageup**：上一页；**pagedown**：下一页；**q**：离开；**/str**：向下搜索字符串；**？str**：向上搜索字符串）

**取出前n行**：head [-**n** num] file

**取出后n行**：tail [-**n** num] file

## 用户和用户组管理

**添加用户**：useradd [-**c**：指定一段注释；**d**：指定主目录，若目录不存在则同时使用**m**来创建；**g**：指定用户组；**G**：指定附加组；**s**：指定登录Shell；**u**：指定标识号；**o**：可以与已有标识相同] username

**删除用户**：userdel [-**r**：把主目录一起删除] username

**修改用户**：usermod [同add] username

**用户密码**：passwd [-**l**：禁用账号；**u**：密码解锁；**d**：删除密码] username

**添加新用户组**：groupadd [-**g**：指定组标识号；**o**：可以与已有标识相同] groupname

**删除用户组**：groupdel groupname

**修改用户组**：groupmod [-**n**：新名字] groupname

**登录后切换用户组**：newgrp groupname

**/etc/passwd, group, shadow**