# System
>

## 命令
+ `top`	// 查看进程
+ `defaults write com.apple.finder _FXShowPosixPathInTitle YES;killall Finder`	// 访达显示路径
+ `defaults delete com.apple.finder _FXShowPosixPathInTitle;killall Finder`	// 显示隐藏文件
+ `defaults write com.apple.finder AppleShowAllFiles YES;killall Finder`	// 显示隐藏文件
+ `defaults write com.apple.finder AppleShowAllFiles NO;killall Finder`	// 不显示隐藏文件
+ `ssh -p User@Host`	// 连接服务器
+ `exit`	// 退出服务器
+ `scp -P Port (-r) User@Host:绝对路径 本地绝对路径`	// 下载
+ `scp -P Port (-r) 本地绝对路径 User@Host:绝对路径`	// 上传
+ `sftp -P Port User@Host`	// 建立sftp传输连接，cd代表远程操作，lcd代表本地操作
+ `get (-r) 远程路径 本地路径`	// 下载
+ `put (-r) 本地路径 远程路径`	// 上传
+ `ssh-keygen -R IpAddress`	// 删除远程服务器连接记录

## 配置
+ `nrm -V`
+ `npm -v`
+ `node -v`
+ `vue -V`
+ `python3 --version`
+ `git --version`
+ `npx -v`
+ `conda -V`
+ `brew -v`
+ `youtube-dl --version`
+ `wget -V`
+ `zsh --version`
+ `n -V`
+ `corepack -v`