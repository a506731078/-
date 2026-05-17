# 谷歌云 V2ray (X-ui) 搭建教程

支持的操作系统：**CentOS 7+、Ubuntu 16+、Debian 8+**（操作流程基本一致）

---

## 准备工具

- FinalShell 下载地址：https://www.hostbuf.com/

---

## 1. 开启防火墙

```bash
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT	
iptables -P OUTPUT ACCEPT
iptables -F
apt-get purge netfilter-persistent

reboot
```

---

## 2. 申请 SSL 证书

### Debian/Ubuntu 系统
```bash
apt update -y
apt install -y curl socat
```

### CentOS 系统
```bash
yum update -y
yum install -y curl socat
```

```bash
curl https://get.acme.sh | sh
~/.acme.sh/acme.sh --register-account -m 506731078@qq.com

# 申请证书（请修改为你的域名）
~/.acme.sh/acme.sh --issue -d gph.laosp.top --standalone

# 安装证书（请修改为你的域名）
~/.acme.sh/acme.sh --installcert -d gph.laosp.top --key-file /root/private.key --fullchain-file /root/cert.crt
```

> 证书文件位置：
> - 公钥：`/root/cert.crt`
> - 私钥：`/root/private.key`

---

## 3. 安装 X-ui 面板

```bash
bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)
```

安装时填写证书路径：
- 公钥路径：`/root/cert.crt`
- 密钥文件路径：`/root/private.key`

---

## 4. 安装 BBR 加速

```bash
wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```

---

## 5. 客户端工具

- v2rayN 下载：https://github.com/2dust/v2rayN/releases
- 如果打不开 v2rayN.exe，请安装 [.NET Framework 4.8](https://docs.microsoft.com/zh-cn/dotnet/framework/install/guide-for-developers)

---

**图片存放文件夹**：`Google-Cloud-V2ray/`
