# VPN搭建1 (PDF)

> 📅 由 Word/PDF → Markdown 转换器生成 · 2026-05-17 18:42

---

## 📑 目录
  - [亚马逊云VPN 搭建](#亚马逊云vpn-搭建)
  - [5.重启sshd 服务](#5重启sshd-服务)
  - [6.为root 账户设置密码](#6为root-账户设置密码)
    - [passwd](#passwd)
    - [Aa#112211](#aa112211)
    - [Aa#506731078](#aa506731078)
- [Debian 10 设置固定IP 地址、网](#debian-10-设置固定ip-地址网)
- [关和DNS](#关和dns)
    - [1、设置固定IP 地址、网关](#1设置固定ip-地址网关)
    - [2、设置dns](#2设置dns)
    - [3、重启服务器](#3重启服务器)
    - [至此，固定IP 地址、网关、DNS 配置完成。](#至此固定ip-地址网关dns-配置完成)
    - [##域名##](#域名)
    - [##SSH 远程桌面客户端##](#ssh-远程桌面客户端)
    - [##Debian/Ubuntu 系统安装运行环境执行以下脚本##](#debianubuntu-系统安装运行环境执行以下脚本)
    - [##CentOS 系统安装运行环境执行以下脚本##](#centos-系统安装运行环境执行以下脚本)
    - [##bbr2 加速##](#bbr2-加速)
    - [##Trojan 多用户管理部署程序一键脚本##](#trojan-多用户管理部署程序一键脚本)
    - [安装/更新](#安装更新)
    - [卸载](#卸载)
    - [##VPS 全方位测试脚本##](#vps-全方位测试脚本)
    - [普通模式：](#普通模式)
    - [简单模式：](#简单模式)
    - [完全模式：](#完全模式)
- [内网穿透及各种插件](#内网穿透及各种插件)
- [命](#命)
- [令](#令)
    - [装完后是这个样子~](#装完后是这个样子)
    - [如果你的服务器没有占用80 或443 8080 端口的话，那么直接输入http://ip:8080](#如果你的服务器没有占用80-或443-8080-端口的话那么直接输入httpip8080)
    - [即可登录后台使用了](#即可登录后台使用了)
    - [如果你vps 上的80 或443 8080 端口被占用，比如装了宝塔的小伙伴们，那么就以宝](#如果你vps-上的80-或443-8080-端口被占用比如装了宝塔的小伙伴们那么就以宝)
    - [塔为例，还要做如下操作，ssh 后台输入./nps stop 停止nps](#塔为例还要做如下操作ssh-后台输入nps-stop-停止nps)
    - [然后输入vi /etc/nps/conf/nps.conf 进入nps 配置文件目录并打开编辑，或](#然后输入vi-etcnpsconfnpsconf-进入nps-配置文件目录并打开编辑或)
    - [finalshell 直接按路径打开，把z80 和443 修改成其他端口，保存重新运行即可~](#finalshell-直接按路径打开把z80-和443-修改成其他端口保存重新运行即可)
  - [三、登录你的服务器的SSH 配置NPS 服务端](#三登录你的服务器的ssh-配置nps-服务端)
  - [四、输入服务器的IP 地址加8080 端口号，即可进入NPS 的后台界](#四输入服务器的ip-地址加8080-端口号即可进入nps-的后台界)
  - [面](#面)
    - [默认用户名：admin 默认密码：123](#默认用户名admin-默认密码123)
    - [因为端口被修改，我们需要到宝塔后台做一下反向代理，方法很简单，添加一个新的站](#因为端口被修改我们需要到宝塔后台做一下反向代理方法很简单添加一个新的站)
    - [点，把域名输入进去，点击反向代理，添加端口号，保存即可~](#点把域名输入进去点击反向代理添加端口号保存即可)
    - [然后来到安全这里放行刚才修改的端口~](#然后来到安全这里放行刚才修改的端口)
    - [写教程太累了，还是看视频吧~：点击观看](#写教程太累了还是看视频吧点击观看)
- [frp 后台运行和停止](#frp-后台运行和停止)

## 亚马逊云VPN 搭建

支持的操作系统（CentOS 7+、Ubuntu 16+、Debian 8+），操作流程是一样的。

在第3 步申请SSL 证书的时候，请输入对应系统的命令，其他的是一样的。

亚马逊申请连接：

```yaml
https://portal.aws.amazon.com/billing/signup#/start
```

安装finalshell，下载安装连接：

```yaml
https://www.hostbuf.com/
```

1：开启root 登入

```bash
sudo su 或sudo -i
cd /root
```

修改authorized_keys 文件（即ssh 证书）

```bash
vi .ssh/authorized_keys
```

把ssh-rsa 之前的文件都删除掉了。（要按i 才能删除）

编辑ssh 配置文件

```bash
nano /etc/ssh/sshd_config 或vim /etc/ssh/sshd_config
```

找到PermitRootLogin，把前面的#删除改成下面这样

PermitRootLogin yes

PasswordAuthentication yes

ctrl+x 保存退出选择y 然后回车

## 5.重启sshd 服务

```bash
service sshd restart
```

## 6.为root 账户设置密码

### passwd

### Aa#112211

### Aa#506731078

然后

```bash
reboot
```

重启服务器。可以使用root 用户名配合秘秘登入了

2、开启防火墙

```bash
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT
iptables -F
apt-get purge netfilter-persistent
reboot 重新开始
```

3、申请SSL 证书

```bash
apt update -y
# Debian/Ubuntu 命令
apt install -y curl
# Debian/Ubuntu 命令
apt install -y socat # Debian/Ubuntu 命令
yum update -y
```

#CentOS 命令

```bash
yum install -y curl
```

#CentOS 命令

```bash
yum install -y socat
```

#CentOS 命令

```bash
curl https://get.acme.sh|sh
# Debian/Ubuntu 命令
~/.acme.sh/acme.sh --register-account -m 506731078@qq.com
```

#

Debian`/Ubuntu` 命令

1753067906

#故障真实邮箱成功率上升

```bash
~/.acme.sh/acme.sh --issue -d th.laosp.top --standalone
```

改变你的解析域

```bash
~/.acme.sh/acme.sh --installcert -d th.laosp.top --key-file /root/private.key
```

--fullchain-file `/root/cert.crt`

更换你的解析域名，此步完成后会在VPS root 目录下

看到证书公钥`/root/cert.crt` 及验证文件`/root/private.key`

公钥路径：`/root/cert.crt`

```yaml
密钥文件路径:/root/private.key
```

4、安装X-ui 面板

bash <(curl -Ls `https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)`

5、安装BBR 加速

```bash
wget -N --no-check-certificate
```

"`https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh"` &&

```bash
chmod +x tcp.sh && ./tcp.sh
```

6、安装V2ray，下载链接：

```yaml
https://github.com/2dust/v2rayN/releases
```

1.

`如果打不开v2rayN.exe`,可以安装.NET Framework 4.8，下载链接：

2.

```yaml
https://docs.microsoft.com/zh-cn/dotnet/framework/install/guide-for-d
```

evelopers

# Debian 10 设置固定IP 地址、网

# 关和DNS

Posted on 2020 年5 月28 日by 红人网络

### 1、设置固定IP 地址、网关

```bash
cp /etc/network/interfaces
```

`/etc/network/interfacesbak`

#备份原有配

置文件

```bash
nano /etc/network/interfaces
```

#编辑网网卡配置文件

auto lo

auto enp4s0

#开机自动连接网络，enp4s0 取决于你安装Debian 时系统分

配的interface

iface lo inet loopback

allow-hotplug enp4s0

iface enp4s0 inet static

#static 表示使用固定ip，dhcp 表述使用动态ip

address `192.168.0.166`

#设置ip 地址

netmask `255.255.255.0`

#设置子网掩码

gateway `192.168.0.1`

#设置网关（这个取决于你路由器的设置）

ctrl+o

#回车，保存配置

ctrl+x

#退出

### 2、设置dns

cp

`/etc/resolv.conf`

`/etc/resolv.confbak`

#备份原有dns 配置文件

```bash
nano /etc/resolv.conf
```

#编辑配置文件

nameserver `8.8.8.8`

#设置首选dns（一般在安装Debian 的时候，系统已经

自动设置好了，这一步可以不修改）

nameserver `8.8.4.4`

#设置备用dns

ctrl+o

#回车，保存配置

ctrl+x

#退出

### 3、重启服务器

```bash
systemctl poweroff
```

#重启机器

### 至此，固定IP 地址、网关、DNS 配置完成。

### ##域名##

免费域名：`freenom.c`om

付费域名：`namesilo.c`om

### ##SSH 远程桌面客户端##

finalshell

Windows 版下载地址:`http://www.hostbuf.com/downloads/finalshell_install.exe`

Mac 版,Linux 版安装及教程:`http://www.hostbuf.com/t/1059.html`

### ##Debian/Ubuntu 系统安装运行环境执行以下脚本##

```bash
apt update -y && apt install -y curl && apt install -y socat
```

### ##CentOS 系统安装运行环境执行以下脚本##

```bash
yum update -y && yum update -y && yum install -y socat
```

### ##bbr2 加速##

PS：此代码为全自动安装BBR2 加速，耐心等待安装完成后，将会自动重启你的VPS，

重启完成后即可正常使用。如查看开启状态，待VPS 重启完成再次输入此代码便可查

看。之后即可安装Trojan 多用户管理部署程序一键脚本。

```bash
wget --no-check-certificate -q -O bbr2.sh "https://github.com/yeyingorg/bbr2.sh/raw/m
```

aster`/bbr2.sh`" && chmod +x `bbr2.sh` && bash `bbr2.sh` auto

### ##Trojan 多用户管理部署程序一键脚本##

### 安装/更新

```bash
source <(curl -sL https://git.io/trojan-install)
```

### 卸载

```bash
source <(curl -sL https://git.io/trojan-install) --remove
```

### ##VPS 全方位测试脚本##

PS:不想测试可直接略过

### 普通模式：

```bash
wget -N --no-check-certificate https://raw.githubusercontent.com/91yun/91yuntest/mast
```

er`/test_91yun.sh` && bash `test_91yun.sh`

### 简单模式：

```bash
wget -N --no-check-certificate https://raw.githubusercontent.com/91yun/91yuntest/mast
```

er`/test_91yun.sh` && bash `test_91yun.sh` s

### 完全模式：

```bash
wget -N --no-check-certificate https://raw.githubusercontent.com/91yun/91yuntest/mast
```

er`/test_91yun.sh` && bash `test_91yun.sh` a

# 内网穿透及各种插件

# 命

# 令

wget

-N

--no-check-certificate

```yaml
https://raw.githubusercontent.com/wxfyes/bt/master/kuaijie.sh && bash kuaijie.sh
路由器客户端命令:./npc -server=18.142.180.191:8024 -vkey=12345678 -type=tcp
```

================================================

You Server IP

: `18.136.204.136`

Bind port

: 5443

KCP support

: true

vhost http port

: 10080

vhost https port

: 10443

Dashboard port

: 6443

token

: 12345678

subdomain_host

: `18.136.204.136`

tcp_mux

: true

Max Pool count

: 50

Log level

: info

Log max days

: 3

Log file

: enable

================================================

frps Dashboard

: `http://18.136.204.136:6443/`

Dashboard user

: admin

Dashboard password : admin

================================================

frps status manage : frps {start|stop|restart|status|config|version}

Example:

```yaml
start: frps start
stop: frps stop
restart: frps restart
```

### 装完后是这个样子~

### 如果你的服务器没有占用80 或443 8080 端口的话，那么直接输入http://ip:8080

### 即可登录后台使用了

### 如果你vps 上的80 或443 8080 端口被占用，比如装了宝塔的小伙伴们，那么就以宝

### 塔为例，还要做如下操作，ssh 后台输入./nps stop 停止nps

### 然后输入vi /etc/nps/conf/nps.conf 进入nps 配置文件目录并打开编辑，或

### finalshell 直接按路径打开，把z80 和443 修改成其他端口，保存重新运行即可~

#HTTP(S) proxy port, no startup if empty

http_proxy_ip=`0.0.0.0`

http_proxy_port=808

https_proxy_port=4437

https_just_proxy=true

#default https certificate setting

https_default_cert_file=conf`/server.pem`

https_default_key_file=conf`/server.key`

##bridge

bridge_type=tcp

bridge_port=8024

bridge_ip=`0.0.0.0`

#web

web_host=`a.o.c`om

web_username=admin

web_password=Aa#506731078

web_port = 8089

web_ip=`0.0.0.0`

## 三、登录你的服务器的SSH 配置NPS 服务端

1.我这里用的谷歌云，谷歌云里面centos 系统里面没有安装wget，所以我们需

要安装一下。

```bash
yum -y install wget
```

2.从github 上获取最新版本的nps 服务端

wget

```yaml
https://github.com/cnlh/nps/releases/download/v0.23.1/linux_amd64_s
```

erver.tar.gz

3.进行解压

```bash
tar -zxvf linux_amd64_server.tar.gz
```

4.启动服务端

.`/nps` start

## 四、输入服务器的IP 地址加8080 端口号，即可进入NPS 的后台界

## 面

### 默认用户名：admin 默认密码：123

.`/nps` start 启用

### 因为端口被修改，我们需要到宝塔后台做一下反向代理，方法很简单，添加一个新的站

### 点，把域名输入进去，点击反向代理，添加端口号，保存即可~

### 然后来到安全这里放行刚才修改的端口~

### 写教程太累了，还是看视频吧~：点击观看

穿透宝塔

=====================================================

=============

```yaml
外网面板地址: http://13.215.199.200:8888/a94ba83d
内网面板地址: http://172.31.24.211:8888/a94ba83d
username: nurbx5sg
password: 7e6b0210
```

If you cannot access the panel,

release the following panel port [8888] in the security group

若无法访问面板，请检查防火墙`/安全组是否有放行面板`[8888]端口

=====================================================

=============

# frp 后台运行和停止

weixin_34244102

于2019-01-16 17:49:44 发布

15870

收藏18

文章标签：操作系统shell

版权

centos

1.运行

```bash
nohup ./frps -c frps.ini >/dev/null 2>&1 &
```

或者客户端:

```bash
nohup ./frpc -c ./frpc.ini >/dev/null 2>&1 &
```

2.停止

先找到这个进程

.

```bash
ps -aux|grep frp| grep -v grep
```

.

.

root

3600

0.1

0.1 110188

9484 pts/0

Sl

```yaml
15:04
0:00 ./frpc
```

-c .`/frpc.ini`

.

执行之后如果显示这样则成功了

然后kill -9 进程号

```bash
kill -9 3600
```

阿里泰国服务器宝塔：

=====================================================

=============

```yaml
外网面板地址: http://8.213.193.237:8888/2cd68848
内网面板地址: http://172.30.130.227:8888/2cd68848
username: ofnvxhj1
password: c758d076
```

If you cannot access the panel,

release the following panel port [8888] in the security group

若无法访问面板，请检查防火墙`/安全组是否有放行面板`[8888]端口

=====================================================

=============

