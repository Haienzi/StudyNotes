
## Linux 学习

#### 安装图形化界面

1. 切换到root用户<br>
   `su ` 回车 输入密码
- 查看要安装的图形化界面的种类<br>
  `yum grouplist`
- 可以看到Available Environment Group中倒数第三行，有GNOME Desktop，这就是我们想要的图形化桌面,输入命令<br>
`yum -y groupinstall "GNOME Desktop"`
- 启动图形化界面
`startx`
- 设置开机默认进入<br>
`vi /etc/inittab `<br>
 主要有两种目标
 - multi-user.target:文本界面
 - graphical.target:图形化界面
 <br>

 查询当前默认的设置 <br>
 `systemctl get-default` <br>
 设置当前默认的设置 <br>
 `systemcltl set-default graphical.target`
