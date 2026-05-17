# 谷歌云 V2ray 搭建教程

支持的操作系统 （CentOS 7+、Ubuntu 16+、Debian 8+），操作流程是一样的。在第3步申请SSL证书的时候，请输入对应系统的命令，其他的是一样的。

安装finalshell，下载安装连接：

https://www.hostbuf.com/

## 1、开启防火墙

```bash
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT	
iptables -P OUTPUT ACCEPT
iptables -F
apt-get purge netfilter-persistent

reboot 重新开始
```

## 2、申请SSL证书

```bash
apt update -y       # Debian/Ubuntu 命令
apt install -y curl   # Debian/Ubuntu 命令
apt install -y socat  # Debian/Ubuntu 命令

yum update -y        #CentOS 命令
yum install -y curl    #CentOS 命令
yum install -y socat   #CentOS 命令

curl https://get.acme.sh | sh
~/.acme.sh/acme.sh --register-account -m 506731078@qq.com
#故障真实邮箱成功率上升 

~/.acme.sh/acme.sh --issue -d gph.laosp.top --standalone

# 改变你的解析域

~/.acme.sh/acme.sh --installcert -d gph.laosp.top --key-file /root/private.key --fullchain-file /root/cert.crt
```

更换你的解析域名，此步完成后会在VPS root目录下看到证书公钥`/root/cert.crt`及验证文件`/root/private.key`

## 3、安装X-ui面板

```bash
bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)
```

公钥路径：`/root/cert.crt`  
密钥文件路径: `/root/private.key`

## 4、安装BBR加速

```bash
wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```

## 5、安装V2ray，下载链接：
https://github.com/2dust/v2rayN/releases

## 6、如果打不开v2rayN.exe,可以安装.NET Framework 4.8，下载链接：
https://docs.microsoft.com/zh-cn/dotnet/framework/install/guide-for-developers
