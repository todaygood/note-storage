

解决办法：首先windows键+R，进入运行界面，然后输入regedit然后点击确定，在注册表编辑器中按照途径HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon,查找AutoRestartShell注册表

（找不到可以新建一个注册表在右侧空白的 地方新建dword32位），将其中的数字由1修改为0，这样就可以阻止重启了

Windows+R调出运行界面 在文本框中输入

查看系统服务：services.msc 
查看系统日志：eventvwr.msc
本地组策略，控制很多行为和策略， 命令是gpedit.msc 

https://blog.csdn.net/u014497502/article/details/51438507

## win10 启动超级用户Administrator方法

【命令方式】

Win+X，选择“以管理员身份运行powershell”

启用内置账户
net user Administrator /active:yes

设置账户密码
net user Administrator 这里写密码


# windows 平板电脑

Administrator用户密码是todaygood69 

margin用户密码是todaygood 

Windows10如何在系统中，重装系统？https://jingyan.baidu.com/article/fd8044fa948f891130137a46.html

[Takeown、Cacls、Icacls-文件、文件夹夺权用法](https://blog.csdn.net/wenzhongxiang/article/details/88143281)


## windows 中的类似于sudo的命令（在cmd中以另一个用户的身份运行命令）

linux中我们习惯用sudo命令来临时用另一个用户的身份执行命令。windows中，通常我们需要用管理员权限执行命令的时候通常是 右键->run as administrator。

用着键盘呢，还要切换成鼠标不免有些麻烦。那么windows中有没有类似sudo的命令呢？

还真有，命令是 runas

比如我以administrator用户运行cmd.exe，可以使用如下命令：

runas /user:administrator cmd.exe

## 删除windows old 

rd $windows.old 

## windows 激活方法

直接上淘宝买 永久激活方法，最省事。 

