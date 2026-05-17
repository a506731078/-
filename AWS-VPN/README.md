# 亚马逊云 VPN / X-ui 搭建教程

支持系统：**CentOS 7+、Ubuntu 16+、Debian 8+**

---

## 1. 开启 Root 登录

```bash
sudo su
cd /root

# 编辑 authorized_keys
vi .ssh/authorized_keys

# 修改 sshd_config
nano /etc/ssh/sshd_config
```

修改以下内容：
```bash
PermitRootLogin yes
PasswordAuthentication yes
```

```bash
service sshd restart
passwd          # 设置 root 密码
reboot
```

---

## 2. 开启防火墙

```bash
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT 
iptables -P OUTPUT ACCEPT
iptables -F
apt-get purge netfilter-persistent

reboot
```

---

## 3. 申请 SSL 证书

（步骤与谷歌云相同，修改域名即可）

```bash
~/.acme.sh/acme.sh --issue -d th.laosp.top --standalone
~/.acme.sh/acme.sh --installcert -d th.laosp.top --key-file /root/private.key --fullchain-file /root/cert.crt
```

---

## 4. 安装 X-ui 面板

```bash
bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)
```

---

## 5. 安装 BBR 加速

```bash
wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```

---

## 附加内容

- Trojan 多用户管理
- 内网穿透 (nps / frp)
- 宝塔面板
- Debian 固定 IP 配置 等

**图片存放文件夹**：`AWS-VPN/`
