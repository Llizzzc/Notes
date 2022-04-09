# Conda
>1.[M1配置Conda](https://blog.csdn.net/yc11tentgy/article/details/113469988 "conda")

## 常用命令
+ `conda create --name EnvName python=Version`	// 创建环境
+ `conda activate EnvName`	// 进入环境
+ `conda deactivate`	// 退出环境
+ `conda -V`	// 版本信息
+ `conda search PackageName`	// 搜索包
+ `conda install PackageName`	// 安装包
+ `conda remove PackageName`	// 删除包
+ `conda update`	// 更新conda
+ `conda update --all`	// 更新所有包
+ `conda env -h`	// 环境管理命令帮助
+ `conda env list`	// 列出所有环境
+ `onda remove --name EnvName --all`	// 删除环境
+ `conda list`	// 列出当前环境所有包
+ `conda list -n EnvName`	// 列出指定环境所有包
+ `conda config --set auto_activate_base false`	// 取消默认base环境
+ `conda config --set auto_activate_base ture`	// 激活默认base环境
+ `conda config --show`	// 查看配置
+ `conda init ShellName`	// 为shell初始化conda
