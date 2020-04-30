1.
安装VMWARE，
这个网址下载源文件，https://www.jb51.net/softs/638408.html
这个网址，https://www.kali.org/docs/virtualization/install-vmware-workstation-player-kali-host/安装方法；

卸载，
/usr/lib/vmware-installer/2.1.0# 
运行vmware-installer -u PRODUCT（产品型号）
例如：vmware-installer -u vmware-player

kali@kali:~$ sudo apt install -y git
kali@kali:~$ git clone https://github.com/mkubecek/vmware-host-modules.git
kali@kali:~$ cd vmware-host-modules/
kali@kali:~$ git checkout workstation-15.5.1
kali@kali:~$ make
kali@kali:~$ sudo make install

运行到这个git下载不了；


3.
试着安装virtualbox，
https://www.virtualbox.org/wiki/Linux_Downloads
同样的方法；
https://www.cnblogs.com/zhishuai/p/8007410.html

但是上面有代号，Ubuntu 15.10 代号为wily；Ubuntu 16.04 (LTS)代号为xenial; Ubuntu 19.10 代号为eoan。
查找版本号：lsb_release -c   结果：Codename:	kali-rolling； Codename后面的就是你当前版本代号

但是上面最新版本没有kali的，所以安装旧版本，试一试，virtualbox-6.0
尝试，在这一步，用别人的代号：
......
deb [arch=amd64] https://download.virtualbox.org/virtualbox/debian eoan contrib
......
sudo apt-get install virtualbox-6.0      #旧版本
......
应该试试这些代号，rolling或者kali kali-rolling,现在用别的代号可能有问题
先来把默认的virtualbox卸载掉！嗯，没错！你装了半天的东西卸载掉！
执行命令	
apt-get remove virtualbox

看下自己kaili是基于哪个版本；
https://www.cnblogs.com/lfoder/p/5777899.html
因为kali linux 2.0是基于Debian Jessie定制的系统。所以去官方网站下载Jessis版本的virtualbox
root@192:~# uname -a
Linux 192 5.2.0-kali2-amd64 #1 SMP Debian 5.2.9-2kali1 (2019-08-22) x86_64 GNU/Linux

另一种方法安装；
https://www.jianshu.com/p/52f92ffcdf20

Kali Linux 2.0 发布，该版本带来了新的 4.0 内核，基于 Debian Jessie
    下一代 Debian 正式发行版的代号为 "buster" — 发布时间尚未确定
    Debian 9（"stretch"） — 当前的稳定版
    Debian 8（"jessie"） — 被淘汰的稳定版
    Debian 7（"wheezy"） — 被淘汰的稳定版
    Debian 6.0（"squeeze"） — 被淘汰的稳定版
    Debian GNU/Linux 5.0（"lenny"） — 被淘汰的稳定版
    Debian GNU/Linux 4.0（"etch"） — 被淘汰的稳定版
    Debian GNU/Linux 3.1（"sarge"） — 被淘汰的稳定版
    Debian GNU/Linux 3.0（"woody"） — 被淘汰的稳定版
    Debian GNU/Linux 2.2（"potato"） — 被淘汰的稳定版
    Debian GNU/Linux 2.1（"slink"） — 被淘汰的稳定版
    Debian GNU/Linux 2.0（"hamm"） — 被淘汰的稳定版


使用了jessis之后
The following packages have unmet dependencies:
 virtualbox-6.1 : Depends: libcurl3 (>= 7.16.2) but it is not installable
                  Depends: libpng12-0 (>= 1.2.13-4) but it is not installable
                  Depends: libssl1.0.0 (>= 1.0.1) but it is not installable
                  Depends: libvpx1 (>= 1.0.0) but it is not installable
                  Recommends: libsdl-ttf2.0-0 but it is not going to be installed
                  Recommends: linux-image but it is not installable
E: Unable to correct problems, you have held broken packages.

1.2
deb [arch=amd64] https://download.virtualbox.org/virtualbox/debian buster contrib
最终使用了debian最新版代号，buster似乎可以；下载就是速度慢
Get:1 https://download.virtualbox.org/virtualbox/debian buster/contrib amd64 virtualbox-6.1 amd64 6.1.4-136177~Debian~buster [93.8 MB]
49% [1 virtualbox-6.1 951 kB/93.8 MB 1%]  

之前使用了eoan就是因为速度慢报错；
Connection failed [IP: 23.209.84.31 443]
Fetched 19.8 MB in 1h 0min 22s (5,461 B/s)
E: Failed to fetch https://download.virtualbox.org/virtualbox/debian/pool/contrib/v/virtualbox-6.0/virtualbox-6.0_6.0.18-136238~Ubuntu~eoan_amd64.deb  Connection failed [IP: 23.209.84.31 443]
E: Unable to fetch some archives, maybe run apt-get update or try with --fix-missing?


网速慢，直接下载昵
 https://download.virtualbox.org/virtualbox/debian 

1.3总结一下
根据官网的教程，https://www.virtualbox.org/wiki/Linux_Downloads
第一步： 修改/etc/apt/sources.list，添加以下源；
deb [arch=amd64] https://download.virtualbox.org/virtualbox/debian buster contrib
第二步：安装官网的安装步骤继续；
第三步：安装好后打开，发现只有32位的，开启硬件虚拟化
对于华硕主板，AMD CPU,按F2进入BIOS设置界面，然后，高级->CPU Configuration->SVM设置为enable
SVM是secure virtual machine
1.3.1
virtualbox里面网络链接点击桥接；
这里有如何设置虚拟机网络的；
插网线可以连接，按照以下设置；用我的无线网卡连接有问题；是否因为网卡设置不一样；
在安装之前设置吗？需要虚拟机关闭状态？
https://www.jianshu.com/p/96a3f05f1dfe
1.3.2
start, 
在close里，选择不一样；
用power shut与save machine state保存得到的结果不一样

鼠标在虚拟机里很卡的原因，可以设置；
https://www.ghacks.net/2009/06/17/install-guest-additions-for-a-better-virtualbox-experience/

https://www.ghacks.net/2009/07/29/install-virtualbox-guest-additions-for-windows-7/
