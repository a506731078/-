# 玩客云 Armbian 部署记录

## 常用命令

```bash
reboot
cp ./源文件 /目标文件夹
cp ./* /目标文件夹    # 复制所有文件
```

## 需要工具

- 电脑
- 玩客云主机
- 双公头 USB 数据线
- U盘 / SD卡
- 尖头镊子

---

## 一、刷机流程

### 1. 刷入底包
使用 USB_Burning_Tool 工具刷入 `s805_flash_snail_2.img`

（详细短接方法见原文图片）

### 2. 刷入 Armbian 系统
- 先刷 Armbian 5.88
- 再刷 Armbian 5.9 并执行安装脚本

```bash
cd /boot/install
sudo ./install.sh
```

---

## 二、更换国内源并更新系统

```bash
cp /etc/apt/sources.list /etc/apt/sources.list.backage

nano /etc/apt/sources.list
```

推荐使用中科大、163、清华等镜像源。

```bash
apt update && apt upgrade -y
```

---

## 三、设置固定IP + 挂载U盘/SD卡 + Samba共享

详细配置见下方代码块（固定IP、自动挂载、Samba 配置等）。

---

## 四、安装 Docker + FAST / Portainer 面板

```bash
# FAST 面板
docker run --restart always --name fast -p 8081:8081 -d -v /var/run/docker.sock:/var/run/docker.sock wangbinxingkong/fast
```

```bash
# Portainer 中文版
docker run -d --name=portainer-zh -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock --restart=always 6053537/portainer-ce
```

---

## 五、安装宝塔面板（Docker版）

详细步骤包括创建 macvlan 网络等。

---

## 六、其他安装（OpenWrt、AList、qBittorrent 等）

**图片存放文件夹**：`PlayCloud-Deployment/`
