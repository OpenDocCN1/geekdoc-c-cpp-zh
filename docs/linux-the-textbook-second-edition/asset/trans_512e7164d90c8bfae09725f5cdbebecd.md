

可以保持不变，即使数字地址发生变化。与其 IP 地址一样，互联网上主机的符号名称必须是唯一的。互联网通过使用分层命名方案来允许使用符号名称。符号名称的格式为

```
hostname.domain_name
```

其中 domain_name 是指站点符号名称，由 NIC 维护其列表的各种注册机构分配。hostname 由分配 domain_name 的站点分配并控制。domain_name 由两个（或更多）字符串组成，以句点（.）分隔。域名中最右边的字符串称为顶级域名（TLD）。最右边句点左侧的字符串标识一个组织，可以由组织自行选择并由 NIC 分配给它。如果该字符串已在同一 TLD 下分配给另一个组织，则会分配另一个字符串以保持域名唯一。有三种类型的 TLD：特殊 TLD、通用 TLD（gTLD）和国家代码 TLD（ccTLD）。根据 IANA 的根域数据库（www.iana.org/domains/root/db），截至撰写时，已注册 1,776 个 TLD。这些域的详细信息在表 11.2 中给出。

对于由两个以上字符串组成的域名，剩余的字符串由拥有该域的组织分配。一些示例域名为 www.infinione.com、stanford.edu、intel.com、whitehouse.gov、uu.net、omsi.org、cs.berkeley.edu、www.cam.ac.uk、amazon.com.jp、pucit.edu.pk、www.beaverton.k12.org.us、www.abc.tv、www.nato.int、www.darpa.mil、example.info 和 bbc.co.uk。国家当局为该国域名的左侧分配字符串。图 11.6 说明了域名层次结构。

将主机名附加到域名并以句点分隔，可得到该主机的完全限定域名（FQDN）——例如 cs.stanford.edu，其中 cs 是斯坦福大学计算机科学系中一台主机的名称。然而，互联网上主机的 FQDN 并不总是具有三个部分。大多数组织允许组织内的各个组为其控制并负责的主机选择主要名称。例如，斯坦福大学计算机科学系使用主要名称 cs.stanford.edu，使用 www.cs.stanford.edu 作为其 HTTP 服务器的 FQDN。杜克大学商学院使用主要名称 fuqua.duke.edu，可以为其 Web 服务器使用主机名 www.fuqua.duke.edu。

## 11.5.4 将名称翻译为 IP 地址：域名系统

由于 Internet 软件处理 IP 地址，而人们更喜欢使用符号名称，因此应用程序软件会将符号名称翻译成等效的 IP 地址。这种翻译涉及使用 Internet 提供的一项服务，即域名系统（DNS）。DNS 实现了一个分布式名称到地址映射数据库。一组专用主机运行名为名称服务器的服务器进程，这些进程接收来自应用程序软件（也称为客户端软件；参见第 11.7 节）的请求并协同工作，将域名映射到相应的 IP 地址。每个组织至少运行一个名称服务器，通常是 Berkeley Internet Name Domain（BIND）程序。应用程序使用解析器函数（如 gethostbyname）来调用 DNS 服务。gethostbyname 解析器函数将主机名（简单或完全限定）映射到其 IP 地址，而 gethostbyaddr 将 IP 地址映射到其主机名。

使用 DNS 服务的一种替代且旧的方案是使用静态 hosts 文件，通常为 /etc/hosts。该文件包含域名及其 IP 地址，每行一个。以下命令显示了一个示例 /etc/hosts 文件。

```
$ more /etc/hosts
127.0.0.1      localhost
127.0.0.1      Mint18

# The following lines are desirable for IPv6 capable hosts
::1            ip6-localhost ip6-loopback
fe00::0        ip6-localnet
ff00::0        ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
$
```

这种方案存在两个问题。首先，其实现取决于系统管理员如何配置系统。其次，由于互联网的庞大规模及其当前增长速度，静态文件可能非常庞大。

## TABLE 11.2

Top-Level Internet Domains

| Domain Type | Top-Level Domain | Assigned To/For |
|---|---|---|
| Special | ARPA | Used exclusively for Internet; currently second-e164.arpa, in-addr.arpa, ip6.arpa, uri.arpa, urn.arpa |
| Generic | ACCOUNTANTS | Known TLD, LLC |
|  | ACTOR | United TLD Holdco, Ltd. |
|  | AERO | Reserved for members of air transport industry |
|  | AIRFORCE | United TLD HoldCo, Ltd. |
|  | ARMY | United TLD HoldCo, Ltd. |
|  | ATTORNEY | United TLD HoldCo, Ltd. |
|  | BEER | Top-Level Domain Holdings Limited |
|  | BIKE | Grand Hollow, LLC |
|  | BIZ | Reserved for businesses |
|  | BUILDERS | Atomic Madison, LLC |
|  | CAREERS | Wild Corner, LLC |
|  | CHRISTMAS | Uniregistry, Corp. |
|  | CHURCH | Holly Fields, LLC |
|  | COM | Reserved for commercial organizations |
|  | COOP | Reserved for cooperative associations |
|  | EDU | Reserved for U.S. postsecondary educational institutions that are accredited by an agency on the U.S. Department of Education’s list of Nationally Recognized Accrediting Agencies |
|  | GOV | Reserved for the U.S. government |
|  | INFO | First unrestricted TLD since .com, so it can be used by anyone—businesses, marketers, and so on |
|  | INT | Reserved for organizations established by treaties between governments |
|  | MIL | Reserved for the U.S. military |
|  | MUSEUM | Reserved for museums |
|  | NAME | Reserved for individuals |
|  | NET | Intended for internet service providers (ISPs) and telephone service providers |
|  | ORG | Intended for noncommercial communities but all are eligible to register |
|  | PRO | Restricted to credentialed professionals (this domain is being established) |
|  | … |  |
|  | ZIP | Charleston Road Registry, Inc. |
|  | ZONE | Outer Falls, LLC |
| Country Code | AU | Australia |
|  | DE | Germany (Deutschland) |
|  | FI | Finland |
|  | JP | Japan |
|  | PK | Pakistan |
|  | … |  |
|  | UK | United Kingdom |
|  | US | United States |

![](img/2a18e06cd9c6395e451f26126ecba1fd_313_0.png)

你可以使用 ifconfig 命令查看和设置网络接口参数，包括 IP 地址、localhost、netmask、广播地址和最大传输单元（MTU）。然而，该命令已不再维护，在大多数现代 Linux 系统中已被更现代的 ip 命令取代。它也可以用于在安装后配置网络接口参数并查看其当前设置。你可以使用 ip 命令完成 ifconfig 命令能完成的所有工作，甚至更多。在本节中，我们展示了 ip 命令的几个示例运行，用于在第 17 章第 8.2 节中检查和设置网络接口参数。

Netmask，也称为 subnetmask，是 TCP/IP 使用的位掩码，用于识别主机是否在远程网络上或本地子网上。广播地址由主机中的 IP 层使用，用于向子网上的所有主机或远程网络发送数据报。Ethernet 广播地址为全 1。TCP/IP 网络中的 MTU 是 IP 数据报（数据包）的最大尺寸，取决于用于连接到其他主机的数据链路层技术。

以下是我们在 Linux Mint 机器上运行 ip 的一个示例。ip addr show（或 ip a s）命令的输出显示，你已登录到一台具有 localhost 接口和网络接口 enp2s0 和 eno1 的主机，每个接口都有 IPv4 和 IPv6 地址。对于 IPv4，localhost 为 127.0.0.1，MTU 为 65,536 字节。对于 IPv6，localhost 为 ::1/128。IPv4 网络地址为 202.147.169.195 和 172.16.0.101；每个的 MTU 为 1,500 字节，广播地址分别为 202.147.169.223 和 172.16.255.255。此外，IP 地址 202.147.169.195 与 MAC 地址 00:10:18:30:ee:6e 相关联。对于 IPv6，enp2s0 和 eno1 的外部流量的网络 IP 地址分别为 fe80::67ab:4f1a:21fa:f0f5 和 fe80::e352:b2f4:9833:cebd。

```
$ ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1
link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
inet 127.0.0.1/8 scope host lo
valid_lft forever preferred_lft forever
inet6 ::1/128 scope host
valid_lft forever preferred_lft forever
2: enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
link/ether 00:10:18:30:ee:6e brd ff:ff:ff:ff:ff:ff
inet 202.147.169.195/27 brd 202.147.169.223 scope global enp2s0
valid_lft forever preferred_lft forever
inet6 fe80::67ab:4f1a:21fa:f0f5/64 scope link
valid_lft forever preferred_lft forever
3: eno1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
link/ether 00:10:18:30:ee:6e brd ff:ff:ff:ff:ff:ff
inet 172.16.0.101/24 brd 172.16.255.255 scope global eno1
valid_lft forever preferred_lft forever
inet6 fe80::e352:b2f4:9833:cebd/64 scope link
valid_lft forever preferred_lft forever
```

