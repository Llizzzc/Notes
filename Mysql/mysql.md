# Mysql
> 

## 常用命令
连接到本机的mysql：==mysql -u ___username___ -p==

连接到远程主机的mysql：==mysql -h___IP___ -u ___username___ -p ___pwd___==

启动mysql服务：==sudo /usr/local/mysql/support-files/mysql.server start==

停止mysql服务：==sudo /usr/local/mysql/support-files/mysql.server stop==

重启mysql服务：==sudo /usr/local/mysql/support-files/mysql.server restart==

查看mysql服务状态：==sudo /usr/local/mysql/support-files/mysql.server status==

查看用户权限：==show grants for ___username___@'___host___';==

新增用户：==create user '___username___'@'___host___' identified by '___pwd___';==

赋予权限：==grant ___privilege___ on ___databasename.tablename___ to '___username___'@'___host___' (with grant option可选);==

撤销权限：==revoke ___privilege___ on ___databasename.tablename___ from '___username___'@'___host___';==

用户改名：==update user set User='***newname***' where User = '***username***'==;

修改用户密码：==alter user ‘___username___’@‘___host___’ identified by ‘___pwd___’;==

删除用户：==drop user '___username___'@'___host___';==

刷新权限表：==flush privileges;==

退出mysql：==quit;==

linux下root改密没用：==cd /etc/mysql；grep -r "skip-grant-tables"；grep -r "user=root"；进入mysql，搜索user下的plugin字段是否为auth__socket==

远端连接mysql：==ufw allow 3306；netstat -an ｜ grep 3306；vim /etc/mysql/mysql.conf.d/mysqld.cnf（注释bind-address=127.0.0.1）；重启ubuntu==