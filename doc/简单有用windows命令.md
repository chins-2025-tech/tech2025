## 榨干硬盘空间 

众所周知，清空回收站后，文件并没有真正从硬盘擦除。windows只是标记了这些硬盘空间为空闲。使用一些技术手段就可以恢复被删除文件。如果想从硬盘上彻底擦除文件，我们可以利用`cihper`命令。 它的原理是使用一个巨大的临时文件覆盖掉磁盘空间，使已删除文件再也无法恢复。

比如我榨干D盘空间，/s:后面接一个盘符即可

```
cipher /w /s:D:
```

## 文件加密

`cipher`另一个重要作用是加密和解密文件和文件夹，加密后的文件只能由当前登陆账号查看。文件的密钥与当前账户绑定到了一起，如果某个人获取了文件但是没有密钥，他无法查看内容。

文件加密

```
cipher /e filename.txt
```

文件解密

```
cipher /d filename.txt
```

文件夹加密

```
cipher /e /s:foldername
```

文件夹解密

```
cipher /d /s:foldername
```



接下来介绍三个有用的网络命令，

## 局域网信息

`ipconfig`用来查看家庭路由器组建的局域网IP。这里显示IP地址是电脑的内网IP。网关ip就是路由器的内网ip。比如我可以直接访问路由器IP地址进入路由器的配置页面。

## 公网信息

上一个命令用来查看局域网信息，下一个命令则是查看公网信息。

```
curl ipinfo.io
```

`curl`简单来说是一个命令行的网络请求工具，他请求了[ipinfo.io](https://ipinfo.io/)这个网址，网站则返回了我的公网IP地址。

 

## tracert 链路检查

```
tracert www.baidu.com
```

用来输出从本机到目标服务器经过的所有网络链路信息，可以用来帮助排查网络故障和优化网络性能


## 查看已保存的wifi

管理员身份运行cmd

输入命令

```
netsh wlan show profiles
```
![image.png](/doc/images/250615/1.png)

选择一个wifi查看查看密码，比如这里以KAONM-A0FF7为例：

```
netsh wlan show profile name="KAONM-A0FF7" key=clear
```

 其中的关键内容即为密码

![image.png](/doc/images/250615/2.png)

## 启动IE浏览器

win10/win11目前已经停止支持IE浏览器了，国情原因有些老古董网站可能还是IE浏览器才能正确使用。

新建一个文件，把下面代码复制进去

```
CreateObject("InternetExplorer.Application").Visible=true
```

以.vbs后缀保存文件，比如——IE.vbs。

之后双击我们新建的文件即可打开被隐藏的IE浏览器。

## Windows11 跳过联网，跳过登陆

我对Win11最不爽的地方就是，强制联网强制登陆。重装系统后，如果在不联网的情况下进入到安装界面“让我们为你连接到网络”这一步，到这里就不能再继续了，“下一步”这个按钮是灰的，不能点击，也没有其他任何可以点击的选项。

此时按下键盘上的Shift+F10组合键，调出CMD命令提示符

输入
```
oobe/bypassnro
```
 回车确认，电脑会重启一次，重新进入安装界面。多了一个选项，我没有internet链接，点击即可继续


## 修复系统关键文件

```
sfc /scannow
```

`SFC /SCANNOW`是立即扫描所有受保护的系统文件的命令。该工具可以允许用户扫描所有受保护的系统文件，并且检查系统文件的完整性，然后恢复Windows损坏的系统文件。SFC的命令对维护整个系统文件很有用。
