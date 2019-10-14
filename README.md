# linux-
自己收集并常用的



Linux /dev/sda1磁盘满了，清理办法:

df -lh 
Filesystem      Size  Used Avail Use% Mounted on
udev            3.9G     0  3.9G   0% /dev
tmpfs           789M  9.4M  780M   2% /run
/dev/sda1        28G   27G  6.1M 100% /
tmpfs           3.9G  248M  3.7G   7% /dev/shm
tmpfs           5.0M  8.0K  5.0M   1% /run/lock
tmpfs           3.9G     0  3.9G   0% /sys/fs/cgroup
/dev/sda7       404G  184G  200G  48% /home
tmpfs           789M  128K  789M   1% /run/user/1000
 
两种情况比较多

1.查看/tmp　所占的内存，不想重启，可以手动清理

2./var/log/syslog.1 所占的内存,清空

可以使用下面指令删除30天前的文件

sudo find /var/log/ -type f -mtime +30 -exec rm -f {} \;

３.清理linux系统垃圾还有以下命令
sudo apt-get autoclean 清理旧版本的软件缓存
sudo apt-get clean 清理所有软件缓存
sudo apt-get autoremove 删除系统不再使用的孤立软件
=================================================================================

配置固定IP地址：
1.进入    /etc/network/interfaces
2.编辑：
auto lo
iface lo inet loopback

auto enp2s0                                           # enp2s0 网络接口
iface enp2s0 inet static               	      #配置静态IP            / dhcp   默认（动态）
address 192.168.6.12                            #IP地址
netmask 255.255.255.0                         #子网掩码
gateway 192.168.6.1                             # 默认网关
dns-nameservers 114.114.114.114 8.8.8.8     # NDS地址
******************************************************************************************************************
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static              
address 192.168.0.30               
netmask 255.255.255.0                 
gateway 192.168.0.1                      
dns-nameservers 61.139.2.69

cat /etc/resolv.conf    系统默认dns   ## root权限执行
===========================================================================
禁用ipv6:
vim /etc/sysctl.conf

net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1

sysctl -p
==========================================================================
2路服务器ip固定不上，baidu.com ping不通

sed -i "/^exit/i\echo \"nameserver 114.114.114.114 \" > /etc/resolv.conf" /etc/rc.local
执行后删除/etc/resolv.conf  

systemctl stop NetworkManager
systemctl disable NetworkManager
========================
networking 服务

========================
============================================================================
配置临时ip：
1.查看网口编号
2.    sudo ifconfig enp2s0 192.168.0.230
sudo ifconfig eth0 192.168.0.230
=============================================================================

3.重启服务器【完成】

重启网卡服务：service network restart
重启指定的网卡：ifdown eth0 && ifup eth0
=============================================================================
性能监测工具的安装与使用-netdata

1.sudo curl https://my-netdata.io/kickstart-static64.sh >/tmp/kickstart-static64.sh
2.sudo wget -O /tmp/kickstart-static64.sh https://my-netdata.io/kickstart-static64.sh
3.sudo sh /tmp/kickstart-static64.sh

使用：
kickstart-static64.sh 执行成功后，会自动启动，默认端口为：19999，使用 ip:19999 就能直接访问页面；
本机访问： 127.0.0.1:19999
=============================================================================

sudo chown -R oeasy:oeasy OeasyProxy/  ## 修改权限
chmod +x   ## 赋予执行权限       
777 ## 最高权限
=============================================================================
V8,1 版本算法支持摄像头为：

平台/厂商                      摄像头型号/名称                                                  URL

华为：X3221-C 200万超星光人脸识别红外半球型摄像机                    rtsp://admin:oeasy123@192.168.6.123/LiveMedia/ch1/Media1
海康：DS-2CD2625EFV2-IZS   （不分型号）                            rtsp://admin:oeasy123@192.168.6.123/mpeg4/ch1/sub/av_stream
天地伟业：sdk相同 rtsp相同（不分型号）                            rtsp://admin:oeasy123@192.168.6.123
==================================================================
arp -a ## 查看本局域网所有ip
iftop  查看各个ip占用宽带情况
==================================================================
当 pip 更新至最新版的时候，不管是执行 pip list 还说 pip install packageName 安装包，都会抛出一个异常
Traceback (most recent call last):
  File "/usr/bin/pip3", line 9, in <module>
    from pip import main
ImportError: cannot import name 'main'

编辑 /usr/bin/pip 文件，修改代码
from pip._internal import main

==================================================================
ubuntu测试网速
sudo apt install speedtest-cli
speedtest-cli
===================================================================
