# Linux笔记

1. **安装**

   CentOS-6.5-x86_64-minimal.iso

   vmware workstation 12

   进bios开启cpu virtualization才能正常开启虚拟机

2. **配置**

   内存1g以上，磁盘20g（大数据推荐100g），其他默认

   磁盘是按需分配

   ctrl + alt 可以释放鼠标

   用户root 密码123456

   磁盘分区 /boot ext4 200mb 启动目录

   ​		swap 2048 用于系统内核

   ​		/ ext4 适配最大空间	根目录

   当输入ls出现时，说明安装成功![1546631764091](C:\Users\Luori\AppData\Roaming\Typora\typora-user-images\1546631764091.png)

3. **网络配置**

   ifconfig 查看网络配置

   ![1546631822235](C:\Users\Luori\AppData\Roaming\Typora\typora-user-images\1546631822235.png)

   修改网络配置

   cd /etc/sysconfig/network-scripts/

   vi ifcfg-eth0

   ![1546639056974](C:\Users\Luori\AppData\Roaming\Typora\typora-user-images\1546639056974.png)

   具体配置

   ![1546639018094](C:\Users\Luori\AppData\Roaming\Typora\typora-user-images\1546639018094.png)

   onboot开机启动，改为yes

   按A进入输入模式，底下会弹出insert

   输入BOOTPROTO=static

   设置IPADDR=192.168. _ . _第三个参数参考vmware虚拟网络编辑器，看子网ip第三个字段![1546639337844](C:\Users\Luori\AppData\Roaming\Typora\typora-user-images\1546639337844.png)

   配置子网掩码NETMASK=255.255.255.0

   配置网关，参考虚拟网络编辑器-NAT设置-网关

   配置DNS，如图

![1546639861104](C:\Users\Luori\AppData\Roaming\Typora\typora-user-images\1546639861104.png)

​	保存文件 ESC->：->wq

​	接下来，删除多余的配置文件 70-persistent-net.rules，因为我们已经删除了mac地址与标识码

​	cd /etc/udev/rules.d/

​	rm -f 70-persistent-net.rules

![1546640044521](C:\Users\Luori\AppData\Roaming\Typora\typora-user-images\1546640044521.png)

​	重启后，输入ping www.google.com，ping通说明网络已配置完毕，按ctrl + c退出

4. **创建快照与克隆**

   创建当前快照

   ![1546640281817](C:\Users\Luori\AppData\Roaming\Typora\typora-user-images\1546640281817.png)

   克隆时选择创建链接克隆

   每台虚拟机要修改ip地址，修改ip方式同上，将最后一个字段分别改成102，103，104，并删除相应的70-persistent-net.rules文件

   虚拟机改名方式如下，修改HOSTNAME字段即可

   cd /etc/sysconfig/

   vi network

   ![1546640812096](C:\Users\Luori\AppData\Roaming\Typora\typora-user-images\1546640812096.png)

   ![1546640839162](C:\Users\Luori\AppData\Roaming\Typora\typora-user-images\1546640839162.png)

   然后重启，输入init 6

5. **XShell与linux命令**

   输入ssh root@192.168.78.101 连接虚拟机，虚拟机此时必须开机

   type 解释命令的作用

​	type ifconfig ![1546641958122](C:\Users\Luori\AppData\Roaming\Typora\typora-user-images\1546641958122.png)

​	type -a ls -a表示ls是代称，不用输入全命令

​	cat ifconfig 查看文件，全是乱码，因为ifconfig是二进制文件

​	file ifconfig 查看文件信息，ELF表示该文件是二进制![1546642102898](C:\Users\Luori\AppData\Roaming\Typora\typora-user-images\1546642102898.png)

​	外部命令包括ifconfig这种二进制文件，也包括yum这种文本文件（python代码)

​	内部命令包括cd这种基本命令

​	shell的组成如图：

![1546642630977](C:\Users\Luori\AppData\Roaming\Typora\typora-user-images\1546642630977.png)

​	环境变量 echo $PATH， echo表示打印输出

​	帮助手册 man表示外部命令，help表示内部命令

​	因为是精简版系统，所以没有man命令，此时需要安装这个包，使用yum install man -y安装， -y表示yes

​	此外还要额外安装 yum install man-pages -y，支持更多的命令

​	man进入文档之后，enter换行，b往前翻，空格切屏，ctrl+z退出

​	此外，想查看具体的内部命令，可以用man 2 read

![1546644514554](C:\Users\Luori\AppData\Roaming\Typora\typora-user-images\1546644514554.png)

​	whereis 能够定位文件的位置，包括其配置文件

​	$LANG表示系统语言，可以用echo查看

​	vi表示编辑文件

​	ll表示详细显示当前文件夹的文件

​	ps -fe 查看进程列表

​	linux可以定义变量 abc=123, echo $abv输出123，定义数组是 c=(1 2 3),输入echo ${c[1]}输出2	

​	echo $$ 显示当前shell的pid

​	hash 用于缓存之前的命令，减少重复访问磁盘，先从path里面找，找到后缓存起来。hash -r 表示清除缓存。

​	df -h表示系统磁盘分区