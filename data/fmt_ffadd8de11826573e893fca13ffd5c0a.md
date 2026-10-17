
```
uart:~
[00:00:00.357,086] <inf> wifi_nrf: Firmware (v1.2.8.1) booted
successfully
[00:00:00.516,204] <inf> fs_nvs: 6 Sectors of 4096 bytes
[00:00:00.516] <inf> fs_nvs: alloc wra: 0, fe8
[00:00:00.535] <inf> fs_nvs: data wra: 0, 0
*** Booting Zephyr OS build v3.99-ncs1-1 ***
Starting nrf7002dk_nrf7001_nrf5340_cpuapp with CPU
frequency: 128 MHz
[00:00:00.516,262] <inf> wpa_supp: Successfully initialized
wpa_supplicant
uart:~$
```

# 第 12 章 ZEPHYR RTOS WI-FI 应用

`uart~$ wifi connect BTBhub6-35MR passphrase`

Connection requested

[00:05:39.711,303] <inf> wpa_supp: wlan0: CTRL-EVENT-DSCP-POLICY: clear_all

[00:05:41.388,397] <inf> wpa_supp: wlan0: SME: Trying to authenticate with e8:ad:a6:e0:81:22 (SSID='BTBhub6-35MR') freq=2462 MHz)

[00:05:41.391,326] <inf> wrf_nrf: wrf_nrf_wpa_supp_authenticate:Authentication request sent successfully

[00:05:41.652,191] <inf> wpa_supp: wlan0: Trying to associate with e8:ad:a6:e0:81:22 (SSID='BTBhub6-35MR' freq=2462 MHz)

[00:05:41.657,806] <inf> wrf_nrf: wrf_nrf_wpa_supp_associate: Association request sent successfully

[00:05:41.673,492] <inf> wpa_supp: wlan0: Associated with e8:ad:a6:e0:81:22

[00:05:41.673,553] <inf> wpa_supp: wlan0: CTRL-EVENT-SUBNET-UPDATE status=0

[00:05:42.694,183] <inf> wpa_supp: wlan0: WPA: Key negotiation completed with e8:ad:a6:e0:81:22 [PTK=CCMP GTK=CCMP]

[00:05:42.694,305] <inf> wpa_supp: wlan0: CTRL-EVENT-CONNECTED - Connection to e8:ad:a6:e0:81:22 completed id=0[00:05:49.830,993] <inf> net_dhcp: Received: 192.168.1.87 uart~$ wifi status

Status: successful

State: COMPLETED

Interface: WIFI (802.11n/HT)

SSID: BTBhub6-35MR

BSSID: E8:AD:A6:E0:81:22

Band: 2.4GHz

Channel: 11

Security: WPA2-PSK

RSSI: -73

Beacon Interval: 100

DTIM: 3

`uart~$ net ipv4`

IPv4 support : enabled

IPv4 fragmentation : disabled

Number of IPv4 interfaces in the system : 1

Number of unicast IPv4 addresses per network : 1

Number of multicast IPv4 addresses per network : 1

IPv4 addresses for interface 1 (0x2000a8) (Ethernet)

| Type | State (sec) | Address |
| --- | :--- | :--- |
| --- | preferred | 192.168.1.87/255.255.255.0 |

`uart~$ dns google.com`

Query for 'google.com' sent.

dns: All received

`uart~$ ping 142.250.187`

28 bytes from 142.250.187 to 192.168.1.87: icmp_seq=1 ttl=117 time=24 ms

28 bytes from 142.250.187 to 192.168.1.87: icmp_seq=2 ttl=117 time=16 ms

28 bytes from 142.250.187 to 192.168.1.87: icmp_seq=3 ttl=117 time=20 ms

uart:~

To ping a PC on a Wi-Fi network, turn the private firewall off (for testing purposes) and then try to:

`uart~$ ping 192.168.166`

28 bytes from 142.250.187 to 192.168.1.87: icmp_seq=1 ttl=128 time=14 ms

28 bytes from 142.250.187 to 192.168.1.87: icmp_seq=2 ttl=128 time=13 ms

28 bytes from 142.250.187 to 192.168.1.87: icmp_seq=3 ttl=128 time=14 ms

uart:~

If the private firewall is on the ping will fail.

`uart~$ ping 192.168.1.86`

PING 192.168.1.86

Ping timeout

uart:~

The code in main relevant to the nRF7002 board is quite simple.

```c
#ifdef CONFIG_NET_CONFIG_SETTINGS
/* With the code as written
DHCPv4 always starts on the Wi-Fi interface
independent of the ordering.
*/
const struct device *dev = device_get_binding("wlan0");

struct net_if *wifi_iface = net_if_lookup_by_dev(dev);
/* As both are Ethernet, need to set a specific interface*/
net_if_set_default(wifi_iface);
net_config_init_app(dev, "Initializing network");
#endif
```

The `prj.conf` file contains a great deal of network configuration, memory, protocol stack, and shell configuration entries and is shown here:

```ini
CONFIG_WIFI=y
CONFIG_WIFI_NRF70X=y

# WPA supplicant
CONFIG_WPA_SUPP=y
CONFIG_NET_L2_WIFI_SHELL=y

# System settings
CONFIG_NEWLIB_IBC=y
CONFIG_NEWLIB_IBC_N=n

# Networking
CONFIG_NET_WORKING=y
CONFIG_NET_SOCKETS=y
CONFIG_NET_LOG=y
CONFIG_NET_IPV6=y
CONFIG_NET_IPV4=y
CONFIG_NET_UDP=y
CONFIG_NET_TCP=y
CONFIG_NET_DHCP4=y
CONFIG_DNS_RESOLVER=y

CONFIG_NET_STATISTICS=y
CONFIG_NET_STATISTICS_WIFI=y
CONFIG_NET_STATISTICS_USER_API=y

CONFIG_NET_PKT_RX_COUNT=8
CONFIG_NET_PKT_TX_COUNT=8

# Below section is the primary contributor to SRAM and is currently
# tuned for performance, but this will be revisited in the future.
```

```ini
CONFIG_NET_BUF_RX_COUNT=16

CONFIG_NET_BUF_TX_COUNT=16

CONFIG_NET_BUF_DATA_SIZE=16

CONFIG_NRF700X_RX_NUM_BUFS=16

CONFIG_NRF700X_MAX_TX_AGGREGATION=4

# nRF700x is main consumer: (16 + 8) * 16 = ~40KB

control path (experimental)
```

```ini
CONFIG_HEAP_MEM_POOL_SIZE=80000

CONFIG_NET_TC_COUNT=1

CONFIG_NET_IF_UNICAST_IPV4_ADDR_COUNT=4

CONFIG_NET_IF_MCAST_IPV6_ADDR_COUNT=5

CONFIG_NET_MAX_CONTEXTS=5

CONFIG_NET_IF_SYNC=y

CONFIG_NET_L2_ETHERNET=y

CONFIG_MAIN_STACKS=y
```

## Basic TCP/IP Application Programming

A Wi-Fi access point has hub-like behavior as well as bridge-like behavior. Only one frame can be successfully transmitted at a time, and collisions do occur, as is the case for a hub. An access point must receive an entire frame before forwarding it, and the frame is forwarded or filtered based on the destination MAC address, which is bridge-like behavior. The wireless clients associated with an access point (AP) constitute a Local Area Network (LAN), and it is possible to configure these clients with static (manually configured) IP addresses. An alternative is to configure the client IP addresses dynamically using the DHCP protocol. One way to do this would to set up a DHCP server on the local Wi-Fi LAN. Alternatively, if the access point is combined with a router (i.e., part of a Wi-Fi router) it is possible to makeuse of the DHCP server on the router itself. More complex Wi-Fi setups can be created using APs that can act as mesh repeaters [6], for example, using Cisco Meraki MR access points. Because repeaters also support wired clients plugged into their wired interfaces, they can also be used to bridge remote LAN

# 第 12 章 ZEPHYR RTOS WI-FI 应用

连接到主网的网段。通过这种方法，可以部署大型 Wi-Fi 网络，例如在办公室或仓库大楼中。

一旦基于 nRF7002 的设备分配了 IP 地址，就可以在该设备上构建标准的 TCP/IP 应用程序（包括客户端和服务器应用程序）并运行它们。在接下来的章节中，将探索实现相对简单的 TCP 和 UDP 客户端与服务器的应用。这些示例基于 nRF Connect SDK sta（基站）示例以及来自 "abluethinginthecloud" (https://github.com/abluethinginthecloud/nrf7002-bsd-sockets-example) 的 BSD socket 编程案例研究。

## nRF Connect SDK Wi-Fi sta 示例的结构化探索

Station 示例位于 nRF Connect SDK 仓库中的 `v2.5.0/nrf/samples/wifi/sta` 。它展示了如何实现应用代码，使用动态主机配置协议 (DHCP) 配置 IP 地址和 TCP/IP，将 nRF7002 DK 开发板上的 Wi-Fi 基站连接到指定的接入点（AP）。

该示例实现了 LED 支持，用于指示连接和断开事件。

- 当示例连接到接入点时，开始闪烁
- 当示例与接入点断开时，停止闪烁

给定 AP 的 Wi-Fi 凭据必须在 "`prj.conf`" 文件中提供，如下：

- 网络名称 (SSID)
- 使用的密钥管理协议
- 密码

在示例中，默认启用了 Zephyr 的电源管理策略，每当 nRF5340 处理器空闲时，就会进入低功耗模式。

示例使用 DHCP 为 Wi-Fi 接口获取 IP 地址。然而，也可以配置静态 IP 地址以处理没有 DHCP 服务器的网络，或者处理 DHCP 服务器不可用的情况。成功的 DHCP 握手将覆盖默认的静态 IP 地址配置。

默认的静态 IP 地址配置在 `prj.conf` 文件，例如：

```
CONFIG_NET_CONFIG_MY_IPV4_ADDR="192.168.1.98"
CONFIG_NET_CONFIG_MY_IPV4_NETMASK="255.255.255.0"
CONFIG_NET_CONFIG_MY_IPV4_Gw="192.168.1.1"
```

应用程序构建目标是 "`nrf7002dk_nrf5340_cpuapp`" 。`prj.conf` 文件非常大，为了应用程序正常工作，确保配置设置与所使用的 AP 类型匹配至关重要。配置设置列如下：

```
CONFIG_WIFI=y
CONFIG_WIFI_NRF700X=y

# WPA  supplic者
CONFIG_WPA_SUP=y

# 选择与 AP 安全能力匹配的设置
```

```
CONFIG_STA_KEY_MGMT_NONE=y
# CONFIG_STA_KEY_MGMT_WPA2=y
# CONFIG_STA_KEY_MGMT_WPA2_256=y
# CONFIG_STA_KEY_MGMT_WPA3=y
CONFIG_STA_SAMPLE_SSID="Myssid"
CONFIG_STA_SAMPLE_PASSWORD="Mypassword"

# 系统设置
CONFIG_NEWLIB_LIBC=y
CONFIG_NEWLIB_LIBC_N=n

# 网络
CONFIG_NETWORKING=y
CONFIG_NET_SOCKETS=y
CONFIG_NET_LOG=y
CONFIG_NET_IPV4=y
CONFIG_NET_UDP=y
CONFIG_NET_TCP=y
CONFIG_NET_DHCP4=y
CONFIG_NET_PKT_RX_COUNT=8
CONFIG_NET_PKT_TX_COUNT=8

# 这些配置影响 Wi-Fi 的 SRAM 使用
# 可以根据性能需求进行调优
CONFIG_NET_BUF_RX_COUNT=16
CONFIG_NET_BUF_TX_COUNT=16
CONFIG_NET_BUF_DATA_SIZE=128
CONFIG_HEAP_MEM_POOL_SIZE=153600
CONFIG_NET_TC_TX_COUNT=1
CONFIG_NET_IF_UNICICAST_IPV4_ADDR_COUNT=1
CONFIG_NET_MAX_CONTEXTS=5
CONFIG_NET_CONTEXT_SYNC_RECV=y
CONFIG_INIT_STACKS=y
```

```
CONFIG_NET_L2_ETHERNET=y
CONFIG_NET_CONFIG_SETTINGS=y
CONFIG_NET_CONFIG_INIT_TIMEOUT=0
CONFIG_NET_SOCKETS_POLL_MAX=6

# 内存
CONFIG_MAIN_STACK_SIZE=4096
```
