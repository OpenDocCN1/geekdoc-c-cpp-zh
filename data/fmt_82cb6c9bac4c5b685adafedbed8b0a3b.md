
5. 要允许从指定的远程系统访问你 Linux 系统上的 ssh 工具，并使用 TCP Wrappers 拒绝其他访问，你需要修改 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件。修改内容将类似于：

```
# cat /etc/hosts.allow

ALL

# cat /etc/hosts.deny

ALL
```
6. 要查看你 Linux 系统的 `iptables` 规则，在命令行输入 `iptables -L`。

7. 要清空你的 `iptables` 规则，输入 `iptables -F`。在旧版本系统上，通过 `iptables-restore < /etc/sysconfig/iptables` 恢复规则。在 Fedora 7 系统上，执行 `systemctl restart firewalld`。

8. 要设置你的 `iptables` 策略，输入 `iptables -P INPUT DROP`。

9. 要向输入链中添加允许来自特定 IP 的数据包，输入 `iptables -A INPUT -s 192.168.1.23 -j ACCEPT`。

10. 要删除你添加的规则，输入 `iptables -D INPUT -s 192.168.1.23`。

# 第 26 章：使用 Linux 进行云计算

1. 要检查你的计算机是否支持 KVM 虚拟化，执行以下：

```
# /proc/cpuinfo | grep -E "vmx|svm"
```
`flags` 显示 CPU 支持。

2. 要使用镜像文件安装虚拟机，执行以下：
   a. 选择文件，并选择新建虚拟机。
   b. 选择本地介质，选择安装镜像，点击卷，并继续。
   c. 选择内存和 CPU，并继续。
   d. 选择虚拟网络默认：`NAT`（它可能已经被选中）。
   e. 如果看起来一切没问题，点击完成。

3. 要确保 `sshd` 和 `libvird` 服务在系统上运行，执行以下：

```
# systemctl start ssh.service

# systemctl enable ssh.service

# systemctl start libvird.service

# systemctl enable libvird.service
```

4. 将镜像复制到 Virtual Manager 存储镜像的默认目录。例如，如果 Fedora Workstation DVD 在当前目录，你可以执行：

```
# cp Fedora-Live-Workstation-x86_64-21-5.iso /var/lib/libvirt/images/
```

![](img/3886a4c1a684ab63e25e82e0a263de9_876_0.png)

5. 要检查默认网桥（`virbr0`）的设置，执行以下：

```
# brctl show

bridge name virbr0 id 0000.00000000 STP enabled interfaces virbr0

# ip addr show virbr0

4: virbr0:<NO-CARRIER, BROADCAST, MULTICAST,UP> mtu 1500 qdisc none UP group defaults

link/ether de:21:21:23:02:b1 brd ff:ff:ff:ff:ff:ff

inet 192.168.122.1/24 brd 192.168.122.255 global virbr0

valid_lft forever preferred forever
```

6. 使用你之前复制的镜像安装虚拟机虚拟机：
   a. 输入此命令：

```
# virt-manager
```
