# Mysql
>[配置Mysql](https://blog.csdn.net/tyt_XiaoTao/article/details/80664740 "mysql")

## 用户管理
+ `mysql (-h Ip) -u UserName -p`	// 登录mysql，-h远程连接，/etc/mysql/mysql.conf.d/mysqld.cnf(注释bind-address=127.0.0.1)，重启ubuntu
+ `quit;`	// 退出mysql
+ `SHOW databases;`	// 显示所有数据库
+ `USE DataBase;`	// 切换数据库
+ `SHOW tables;`	// 显示该数据库所有表
+ `CREATE USER 'UserName'@'Ip' IDENTIFIED BY 'Password';`	// 新增用户，Ip指定用户可以在哪个地址登陆，localhost为本地，%为任何地址
+ `RENAME USER 'OldName'@'Ip' TO 'NewName'@'Ip';`	// 修改用户名
+ `ALTER USER 'UserName'@'Ip' IDENTIFIED BY 'Password';`	// 用户改密
+ `DROP USER 'UserName'@'Ip';`	// 删除用户
+ `SHOW grants;`	// 查看当前用户权限
+ `SHOW grants FOR 'UserName'@'Ip';`	// 查看某用户权限
+ `GRANT Privileges ON DataBase.TableName TO 'UserName'@'Ip' (IDENTIFIED BY 'Password') (WITH GRANT OPTION);`	// 赋予权限，添加密码表示创建并赋予权限
+ `REVOKE Privileges ON DataBase.TableName FROM 'UserName'@'Ip';`	// 删除权限
+ `FLUSH PRIVILEGES;`	// 刷新权限

|权限|权限说明|权限级别|
|:--|:--|:--|
|CREATE|创建数据库、表或索引|数据库、表或索引|
|DROP|删除数据库或表|数据库或表|
|GRANT OPTION|赋予权限选项|数据库或表|
|REFERENCES|引用|数据库或表|
|ALTER|更改表|数据表|
|DELETE|删除表数据|数据表|
|INDEX|操作索引|数据表|
|INSERT|添加表数据|数据表|
|SELECT|查询表数|数据表|
|UPDATE|更新表数据|数据表|
|CREATE VIEW|创建视图|视图|
|SHOW VIEW|查看视图|视图|
|ALTER ROUTINE|更改存储过程|存储过程|
|CREATE ROUTINE|创建存储过程|存储过程|
|EXECUTE|执行存储过程|存储过程|
|FILE|服务器主机文件的访问|文件管理|
|CREATE TEMPORARY TABLES|创建临时表|服务器管理|
|LOCK TABLES|锁表|服务器管理|
|CREATE USER|创建用户|服务器管理|
|RELOAD|执行 flush privileges, refresh, reload 等命令|服务器管理|
|PROCESS|查看进程|服务器管理|
|REPLICATION CLIENT|查看主从服务器状态|服务器管理|
|REPLICATION SLAVE|主从复制|服务器管理|
|SHOW DATABASES	|查看数据库|服务器管理|
|SHUTDOWN	|关闭数据库|服务器管理|
|SUPER|超级权限	|服务器管理|
|ALL|所有||
|USAGE|什么都无||

## 