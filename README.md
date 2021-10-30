# 前言

路由器的机型是大麦路由器DW22d型号，主要的刷机和刷固件的流程是先刷Breed系统(其实就相当于电脑的BIOS)，其次刷固件即老毛子改的潘多拉固件(就是控制系统由华硕路由器的控制系统魔改过来)，做完这些即可让路由器支持WiFi翻墙、内网穿透、广告屏蔽等等操作。



# 一、开启路由器的SSH

- 接上路由器的网络，进入路由器的更新界面

```
浏览器输入http://192.168.10.1/upgrade.html
```

- 开启SSH开关并输入密码，其中提示密码错误没关系

```
123 | echo 6c216b27c8c9b051106c969e2077d4e9 > /ezwrt/bin/upgrade_passwd 
```

- 再次进入界面重复上一步操作，输入下列密码

```
123 | echo ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEAmavYNZq5oC5lzN1VCXCTR/wnkGKse+AMWJGjUplAv+IVIrnEM9uQftzLZ6QaZ8L70ABQba4m5Bs6AD6kJfZQnZIEziVbVV9BvX0y4SPL53vXeDW4iUJtUE7v3twpmoWPrxbciXoe8FfaAUT9eyMN2g5L/JCLnVovI60m9sAgFvjNm0jqJxYCUCxovRwGyO8A44vQclAwX8iY5FwJuPn419QGPwBVmX5PqcW1uABBReq/ob/3m5bnQZPjhFhEo/F2AquaVQDsHRoqx3YFXDde4i1WutWMJ1peq+rS1axT01Elm8ELaC0lvfzxkanYON3FCRMUM2p4CNIVj19tgMC+aQ== rsa-key-20200727-dw22d dm > /etc/dropbear/authorized_keys 
```

- 再次打开SSH，输入下列密码点击确定

```
dfc643
```



# 二、SSH连接路由器

- 进入[Putty官网](http://www.putty.be/latest.html)下载Putty的msi安装包
- 下载所用到的breed系统、密钥文件、老毛子潘多拉固件
- 在putty的文件夹下打开pagent.exe，点击add key添加密钥，将dw22d.ppk密钥添加
- 打开putty.exe，输入192.168.10.1并连接，输入root用户进去终端界面
- 输入passwd更改密码
- 解锁mtd否则无法刷机

```
/etc/init.d/uhttpd enable
/etc/init.d/uhttpd start
```



# 三、刷Beed系统

- 浏览器输入http://192.168.10.1/upgrade.html进入更新界面
- 上传固件breed-mt7620-reset13.bin其中文件名和密码后面要对应，密码输入下列

```
password | mtd -x mIp2osnRG3qZGdIlQPh1 -r write /tmp/breed-mt7620-reset13.bin Bootloader
```

- 等待刷机完成后拔掉电源然后首先按住reset键不放的同时插入电源，然后松开等待开机，其中成功后可能路由器上的指示灯不会亮
- 打开http://192.168.1.1/



# 四、刷老毛子固件

- 备份EEPROM和编程器固件
- 进入恢复出厂设置，固件类型选择Config区(公版)，单击执行
- 单击固件更新，选择常规固件--固件，选择上传文件，RT-AC51U-GPIO-12-ji2-128M_3.4.3.9-099.trx
- 刷机后重启，网线插入LAN口，浏览器输入192.168.123.1，登录和密码都是admin
- 刷机成功
- 老毛子固件下载地址[老毛子固件](http://www.nihaodd.com/down/85.php)