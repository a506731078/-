# bsjc

一个以“部署/运维记录”为主的文档仓库，包含：

- **AWS 上搭建 VPN/代理相关环境**的操作记录
- **Google Cloud 上搭建 V2Ray（含 x-ui 面板）**的操作记录
- **玩客云（OneCloud）刷机 + Armbian 部署**的操作记录与常用命令

仓库内容主要来自 Word/Doc 文档转换成 Markdown 的 README（便于在 GitHub 在线阅读与检索）。  
> 由转换器生成的时间在各子目录 README 中可见（例如 2026-05-17）。  

---

## 目录结构

- <!--citation:3-->
  - `README.md`：亚马逊云 VPN 搭建记录（含 SSH 配置、root 登录、防火墙、证书申请、加速/脚本等内容）
  - `VPN搭建.docx`：原始文档

- <!--citation:4-->
  - `README.md`：谷歌云 V2Ray 搭建记录（iptables、acme.sh 证书、x-ui 面板等）
  - `谷歌云搭建.docx`：原始文档

- <!--citation:5-->
  - `README.md`：玩客云部署/刷机记录（刷底包、刷 Armbian、换源、常用命令等）
  - `玩客云部署记录.doc`：原始文档

---

## 内容概览（你能在这里找到什么）

### 1) AWS-VPN（亚马逊云相关）
该部分主要是 VPS 初始化与连通性配置的记录，例如：

- 开启/配置 root 登录与 SSH 配置（`sshd_config`）
- 重启 sshd、设置 root 密码、重启服务器
- 使用 iptables/清理防火墙规则
- 通过 `acme.sh` 申请 SSL 证书（standalone 模式）
- 以及一些常用脚本/加速/测试/内网穿透工具的笔记（在文档目录中有目录项）

> 注意：文档中出现了示例密码、默认账号等内容，请自行替换并避免在公网泄露。

---

### 2) Google-Cloud-V2ray（谷歌云 + V2Ray/x-ui）
该部分包含：

- iptables 放行/清理规则的命令
- `acme.sh` 注册与签发证书、证书文件输出路径（如 `/root/private.key`、`/root/cert.crt`）
- 通过脚本安装 x-ui 面板（README 中给出了安装脚本调用方式）

> 注意：域名、邮箱等为示例/记录用途；请替换成你自己的真实配置。

---

### 3) PlayCloud-Deployment（玩客云）
该部分是一份偏“实操流程”的刷机与系统部署笔记，包含：

- 所需工具清单（双公头 USB 线、U 盘/SD 卡、镊子等）
- 刷底包、写入 Armbian（5.88 -> 更新到 5.9）的流程
- SSH 登录说明与安装脚本执行示例
- Debian/Armbian 换源、系统更新的常用操作
- 常用命令（如 `reboot`、`cp` 等）

---

## 使用方式

建议按“目标”进入对应目录阅读：

- AWS 上搞 VPN/代理环境：进入 `AWS-VPN/README.md`
- Google Cloud 上搭 V2Ray/x-ui：进入 `Google-Cloud-V2ray/README.md`
- 玩客云刷机与部署：进入 `PlayCloud-Deployment/README.md`

---

## 安全与合规提醒（强烈建议先看）

1. **不要把真实密码/私钥/证书/面板口令提交到公开仓库**  
   文档里出现过 root 密码示例、默认账号密码等内容；请在实际部署时全部替换，并在仓库中脱敏处理。

2. **云服务器安全基线建议**
   - 禁用 root 远程密码登录（改用密钥 + sudo）
   - 只放行必要端口（不要“全 ACCEPT”长期运行）
   - 面板（如 x-ui）务必改默认端口/默认密码，并加防火墙/访问控制
   - 定期更新系统与组件

3. **遵守当地法律法规与云厂商条款**  
   本仓库为个人部署记录与学习用途；请在合法合规前提下使用。

---

## 许可（License）

仓库当前未声明 License（默认视为“未授权”，他人不可随意复制/再分发）。  
如需开源，建议补充 `LICENSE` 文件并在 README 中注明。

---

## 致谢

- 文档里使用到的一些脚本/工具（例如 acme.sh、x-ui 等）归其各自作者与项目所有。
