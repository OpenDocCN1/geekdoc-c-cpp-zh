
在任何情况下，都使用 `dig` 命令检查 DNS 服务器是否能够解析：

```bash
google.com 91941 IN NS ns3.google.com.
;; Query time: 0 msec
;; SERVER: 8.8.8.8#53(8.8.8.8)
;; WHEN: Mon Apr 30 13:57:44 2012
;; MSG SIZE rcvd: 276
```

## 9. 创建自定义路由

要创建一个自定义路由将目标为 `192.168.99.0/255.255.255.0` 的流量重定向到本地网络 `192.168.0.5`（确保位置未使用 `10.0.99` 网络），请执行以下操作：

确定你的网络接口名称。对于 RHEL，第一个接口可能是 `eth0`。在这种情况下，运行：

```bash
# vi /etc/sysconfig/network
```

在该文件中添加以下行：

```
DEVICE=eth0
IPADDR=192.168.0.5
NETMASK=255.255.255.0
GATEWAY=192.168.0.1
```

重启网络并运行 `route` 查看路由是否已激活：

```bash
# service network restart
route
```

| Destination | Gateway Genmask Flags Metric Use Interface |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0.0.0.0 | 192.168.0.1 | 0.0.0.0 | UG | 0 | 0 | eth0 |
| 192.168.0.0 | 0.0.0.0 | 255.255.255.0 | UG | 0 | 0 | eth0 |

# 第 15 章：启动与停止服务

### 1. 确定初始化系统

要确定当前正在哪个初始化系统，请考虑：
* 如果你的 Linux 服务器运行以下之一：RHEL 版本 6、Fedora 9 到 14、Ubuntu 版本 6-14.10 或 opensuse 版本 11.3-12.1，且 `strings` 命令显示如下例所示的 Upstart 初始化进程，则使用 Upstart：
* `$ strings /bin/init | grep -i upstart`
  `upstart-develists.ubuntu.com`
  `UPSTART CONDIR`
  `UPSTART_NO_SESSIONS`

* 如果你的 Linux 服务器运行 Fedora 15 或更高、RHEL 7、Ubuntu 15.04 或 OpenSE 12.02 或更高，则拥有 systemd。在某些情况下，PID 1 是 systemd。在其他情况下，PID 1 是 init 守护进程。要判断是否为 systemd 守护进程，可以运行 `strings` 命令显示 systemd 显示：
* `$ strings /bin/init | grep -i systemd`
  `systemd.unit=`
  `systemd.log_target=`
  `systemd.log_level=`

* 如果你的 init 守护进程是 Upstart 守护进程或 systemd，则可能是 SysVinit 或 BSD init 守护进程。

### 2. 管理服务的工具

管理服务的工具取决于使用的初始化系统。尝试运行 `initctl`、`systemctl` 和 `service` 命令来确定系统中 ssh 服务的初始化脚本类型：
* 如下所示的积极结果意味着 sshd 已转换为 Upstart：
* `# initctl status ssh`
  `ssh start/running, process 2390`

对于 systemd，此处所示的积极结果意味着 sshd 已转换为 systemd：

```
# systemctl status sshd.service

sshd.service - OpenSSH server daemon

Loaded: loaded (dead;; enabled)

Active: active (running) since Mon, 30 Apr 2015 12:35:20...
```

如果你在上述测试中没有看到积极结果，请执行以下针对 SysVinit 守护进程的命令。如果存在 SysVinit 且上述测试结果为极，说明 sshd 仍在使用 SysVinit 守护进程。

```
# service status
sshd (pid 2390) is running...
```

### 3. 确定运行级别

要确定你服务器之前和当前的运行级别（runlevel），请使用 `runlevel` 命令，它适用于所有初始化守护进程：

```
$ runlevel
N3
```

### 4. 更改默认运行级别或目标单元

要更改 Linux 服务器上的默认运行级别或目标单元（target unit），你可以执行以下操作（取决于服务器的初始化守护进程）：

- 对于 SysVinit，编辑文件 `/etc/initab`，并将 `id:default:` 行中的 `#` 改为 2、3、4 或 5。
- 对于 Upstart，编辑文件 `/etc/initab`，并将 `id:default:` 行中的 `#` 改为 2、3、4 或 5。
- 对于 systemd，将 `default.target` 符号链接更改为所需的运行级别，即 2、3、4 或 5。以下显示了如何将目标单元的符号链接更改为 `runlevel3.target`。

```
# ln -sf /lib/systemd/system/runlevel3.target /etc/systemd/system/default.target
runlevel3.target
```

### 5. 列出运行中的服务

要列出你服务器上运行（或活动）的服务，你需要根据正在使用的初始化守护进程使用不同的命令。

对于 SysVinit，使用示例所示的 `service` 命令：

```
# service --status-all | grep running...
anacron (pid 2162) is running...
atd (pid 2172) is running...
```

对于 Upstart，使用 `initctl` 命令。不过，务必同时也使用 `service` 命令，因为并不是所有服务都已迁移到 Upstart：

```
# initctl list | grep start/running
tty (dev/tty3) start/running, process 1163
```

## 附录 B：练习答案

`# service --status-all | grep running`
`abrtd (pid 1118) is running...`
`...`

- 对于 systemd，使用如下的 `systemctl` 命令：

```
# systemctl list-unit-files --type=service | grep -v disabled
UNIT FILE STATE
abrtd-ccpp.service enabled
abrtd-oops.service enabled
...
```

- 6. 要列出你 Linux 服务器上运行（或活动）的服务，请根据答案 5 中针对你服务器使用的初始化守护进程确定的相应命令。

- 7. 对于每个初始化守护进程，以下命令可显示特定服务器的状态：
对于 SysVinit，使用 `service service_name status` 命令。
对于 Upstart，使用 `initctl status service_name` 命令。
对于 systemd，使用 `systemctl status service_name` 命令。

### 8. 显示 cups 守护进程状态

要显示你 Linux 服务器上 cups 守护进程的状态，请使用以下命令：
对于 SysVinit：
`# service cups status`
`cupsd (pid 8236) is running...`
对于 Upstart：
`# initctl status cups`
`cups start/running, process 2390`
记住，如果某个服务尚未迁移到 Upstart，你需要使用 `service` 命令而不是 `initctl`。
对于 systemd：
`# systemctl status cups.service`
`cups.service - CUPS Printing Service`
`Loaded: loaded (/lib/systemd/system/cups.service; enabled)`
`Active: active (running) since Tue, 01 May 2015 04:43:5...`
`PID: 17003 (cupsd)`
`CGGroup: name=systemd:system/cups.service`
`17003 /usr/bin/cupsd -f`

### 9. 重启 cups 守护进程

要尝试重启你 Linux 服务器上的 cups 守护进程，请使用以下命令：
对于 SysVinit：
`# service cups restart`
`Stopping cups: [ OK ]`
`Starting cups: [ OK ]`

- 对于 Upstart：
`# initctl restart cups`
`cups start/running, process 2490`

- 记住，如果某个服务尚未迁移到 Upstart，你需要使用 `service` 命令而不是 `initctl`。

- 对于 systemd：
`# systemctl restart cups.service`

### 10. 重载 cups 守护进程

要尝试重载你 Linux 服务器上的 cups 守护进程，请使用以下命令：

- SysVinit
`# service cups reload`
`Reloading cups: [ OK ]`

- 对于 Upstart：
`# initctl reload cups`

记住，如果某个服务尚未迁移到 Upstart，你需要使用 `service` 命令而不是 `initctl`。

- 对于 systemd，这是一个陷题。你无法在 systemd Linux 服务器上重载 cups 守护进程！

```
# systemctl reload cups.service
Failed to issue method call: Type reload is not applicable for unit cups.service.
```

## 第 16 章：配置打印服务器

- 1. 对于每个初始化守护进程，以下命令可显示特定服务器的状态：
对于 SysVinit，使用 `service service_name status` 命令。
对于 Upstart，使用 `initctl status service_name` 命令。
对于 systemd，使用 `systemctl status service_name` 命令。

### 8. 显示 cups 守护进程状态

要显示你服务器上 cups 守护进程的状态，请使用以下命令：
对于 SysVinit：
`# service cups status`
`cupsd (pid 8236) is running...`
对于 Upstart：
`# initctl status cups`
`cups start/running, process 2390`
记住，如果某个服务尚未迁移到 Upstart，你需要使用 `service` 命令而不是 `initctl`。
对于 systemd：
`# systemctl status cups.service`
`cups.service - CUPS Printing Service`
`Loaded: loaded (/lib/systemd/system/cups.service; enabled)`
`Active: active (running) since Tue, 01 May 2015 04:43:5...`
`PID: 17003 (cupsd)`
`CGGroup: name=systemd:system/cups.service`
`17003 /usr/bin/cupsd -f`

### 9. 重启 cups 守护进程

要尝试重启你 Linux 服务器上的 cups 守护进程，请使用以下命令：
对于 SysVinit：
`# service cups restart`
`Stopping cups: [ OK ]`
`Starting cups: [ OK ]`

- 对于 Upstart：
`# initctl restart cups`
`cups start/running, process 2490`

- 记住，如果某个服务尚未迁移到 Upstart，你需要使用 `service` 命令而不是 `initctl`。

- 对于 systemd：
`# systemctl restart cups.service`

### 10. 重载 cups 守护进程

要尝试重载你 Linux 服务器上的 cups 守护进程，请使用以下命令：

- SysVinit
`# service cups reload`
`Reloading cups: [ OK ]`

- 对于 Upstart：
`# initctl reload cups`

记住，如果某个服务尚未迁移到 Upstart，你需要使用 `service` 命令而不是 `initctl`。

- 对于 systemd，这是一个陷题。你无法在 systemd Linux 服务器上重载 cups 守护进程！

```
# systemctl reload cups.service
Failed to issue method call: Type reload is not applicable for unit cups.service.
```

*(注：由于原文中存在大量重复内容，译文已按要求对所有出现的内容进行了翻译)*

# 附录 B：练习答案

在 RHEL 6 或更版本中，
```bash
# service httpd start
# chkconfig on
```

### 4. 查看 httpd 监听端口

使用 `netstat` 命令查看 httpd 服务器监听哪些端口，请使用以下命令：
```bash
# netstat -tupn | grep httpd
tcp6 0 0 :::80* LISTEN 2496/httpd
tcp6 0 0 :::443* LISTEN 2496/httpd
```

### 5. 从远程浏览器连接 Apache

要从本地系统外的浏览器连接到 Apache Web 服务器，请通过检查防火墙、SELinux 和其他安全功能来解决遇到的任何问题。
如果您没有设置 DNS，请使用服务器的 IP 地址从远程浏览器查看您的 Apache 服务器，例如 `http://192.168.0.1`。如果无法连接，请在运行 Apache 服务器的系统上执行每个步骤后，重新在浏览器中连接服务器：
```bash
# iptables -F
# setenforce 0
# chmod 644 /var/www/html/index.html
```

`iptables -F` 命令临时清除防火墙规则。如果之后成功连接 Web 服务器，您需要添加新的防火墙规则来开放 tcp 端口 80 和 443。对于使用 `firewalld` 服务的系统，请通过点击防火墙窗口中端口旁边的复选框来实现。对于运行 `iptables` 服务的系统，请在最后一个 DROP 或 REJECT 规则之前添加以下规则：
```bash
-A INPUT -m state NEW -m tcp -p tcp --dport 80 -j ACCEPT
-A INPUT -m state NEW -m tcp -p tcp --dport 443 -j ACCEPT
```

`setenforce 0` 命令将 SELinux 置于许可模式（permissive mode）。如果之后成功连接 Web 服务器，您可能需要修复 SELinux 上下文和/或布尔值问题（在这种可能是文件上下文）。执行以下操作：
```bash
# chcon --reference=/var/www/html/var/www/html/index.html
```
如果 `chmod` 命令有效，则意味着 Apache 用户和组没有对该文件的读取权限。您应该可以直接启用这些新权限。

### 6. 创建 RSA 密钥和自签名 SSL 证书

使用 `openssl` 或类似命令创建您的私 RSA 密钥和自签名 SSL 证书，请执行以下操作：
```bash
# yum install openssl
# cd /etc/pki/tls/private
# openssl genrsa -out out-server.key 1024
# chmod 600 server.key
```

```bash
# cd /etc/pki/tls/certs
# openssl_req -new -x509 -nodes -sha -days 365 \
# -key /etc/pki/tls/private/server.key \
# -out server.crt
Country Name [letter code] [AU]: US
State or Province Name (full name) [] [Some-State]: NJ
Locality Name (eg, city) []: Princeton
Organization Name (eg, company) [Internet Widgets Pty] LTD:TEST USE ONLY
Organizational Unit Name (eg, section) [:TEST USE ONLY
Common Name (eg, YOUR name) [:secure.example.org
Email Address [:dom@example.org
```

现在您应该有一个 `/etc/pki/tls/private/server.key` 密钥文件和一个 `/etc/pki/tls/certs/server.crt` 证书文件。

### 7. 配置 Apache 使用密钥和证书

配置您的 Apache Web 服务器使用您的密钥和自签名证书来保护服务器（HTTPS），请执行以下操作：

- a. 编辑 `/etc/httpd/conf.d/ssl.conf` 文件，将密钥和证书的位置更改您刚刚创建的位置：
```ini
