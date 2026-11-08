

## 第二部分 复习命令 思维导图答案

![](img/79473ea15699e01619d2aa789f5bd43b_1021_0.png)

## 第三部分 复习关键术语 思维导图答案

![](img/79473ea15699e01619d2aa789f5bd43b_1022_0.png)

## 第三部分 复习命令 思维导图答案

![](img/79473ea15699e01619d2aa789f5bd43b_1023_0.png)

![](img/79473ea15699e01619d2aa789f5bd43b_1023_1.png)

![](img/79473ea15699e01619d2aa789f5bd43b_1023_2.png)

![](img/79473ea15699e01619d2aa789f5bd43b_1023_3.png)

### 第 3 部分 命令

## 第四部分 复习关键术语 思维导图答案

![](img/79473ea15699e01619d2aa789f5bd43b_1025_0.png)

## 第五部分 复习故障排除 思维导图答案

![](img/79473ea15699e01619d2aa789f5bd43b_1026_0.png)

## 第五部分 复习命令 思维导图答案

![](img/79473ea15699e01619d2aa789f5bd43b_1027_0.png)

## 第六部分 复习故障排除 思维导图答案

![](img/79473ea15699e01619d2aa789f5bd43b_1030_0.png)

## 第六部分 复习命令 思维导图答案

### 第 6 部分 命令

- 主机
  - 路由器
    - ip host name [tcp-port-number] address [address...]
    - ip domain-lookup
    - ip name-server server-address1 [server-address2...]
    - ip domain-name name
    - ip domain-list name
  - IPv4
    - ipv4 host name [port] address [address...]
    - ipv4 domain-lookup
    - ipv4 name-server server-address1 [server-address2...]
    - ipv4 domain-name name
    - ipv4 domain-list name
  - IPv6
    - ipv6 host name [port] address [address...]
    - ipv6 domain-lookup
    - ipv6 name-server server-address1 [server-address2...]
    - ipv6 domain-name name
    - ipv6 domain-list name

- IPv4 ACL
  - 配置
    - 标准
      - access-list access-list-number {permit|deny} source [source-wildcard]
      - access-list access-list-number {permit|deny} source [source-wildcard] log
      - access-list access-list-number remark remark
    - 扩展
      - access-list access-list-number {permit|deny} protocol source source-wildcard destination destination-wildcard [option]
      - access-list access-list-number {permit|deny} protocol source source-wildcard destination destination-wildcard [option] log
      - access-list access-list-number remark remark
  - 显示
    - show ip access-lists [access-list-number|access-list-name]
    - show ip access-lists [access-list-number|access-list-name] [summary]
    - show ip access-lists [access-list-number|access-list-name] [detail]

- 其他
  - 配置
    - IPv6
      - ipv6 access-list access-list-name
      - ipv6 access-list access-list-name {permit|deny} ...
      - ipv6 access-list access-list-name remark remark
  - 显示
    - show ipv6 access-lists [access-list-name]
    - show ipv6 access-lists [access-list-name] [summary]
    - show ipv6 access-lists [access-list-name] [detail]

- OSPFv3
  - 配置
    - 路由器
      - ipv6 router ospf process-id
      - router-id router-id
      - maximum-paths number-of-paths
      - passive-interface interface
      - [no] default-information originate [always] [metric metric-value] [metric-type type-value] [route-map map-name]
      - [no] distance [admin-distance] [address wildcard-mask]
      - [no] redistribute protocol [process-id] {metric metric-value} [metric-type type-value] [match internal|external 1|external 2] [route-map map-name] [subnets] [tag tag-value]
      - [no] area area-id range ipv6-prefix/prefix-length [advertise|not-advertise] [cost cost]
      - [no] auto-cost reference-bandwidth bandwidth
      - [no] bfd all-interfaces
      - [no] default-metric metric-value
      - [no] summary-prefix ipv6-prefix/prefix-length [not-advertise] [tag tag]
      - [no] timers spf delay hold
      - [no] timers throttle spf spf-start spf-hold spf-max-wait
    - 接口
      - [no] ipv6 ospf process-id area area-id [instance instance-id]
      - [no] ipv6 ospf cost cost
      - [no] ipv6 ospf dead-interval {seconds|minimal hello-multiplier}
      - [no] ipv6 ospf hello-interval seconds
      - [no] ipv6 ospf mtu-ignore
      - [no] ipv6 ospf network {broadcast|point-to-point}
      - [no] ipv6 ospf priority number
      - [no] ipv6 ospf retransmit-interval seconds
      - [no] ipv6 ospf transmit-delay seconds
  - 显示
    - 接口
      - show ipv6 ospf [process-id] interface [interface-type interface-number] [brief]
      - show ipv6 ospf interface [interface-type interface-number] [brief]
    - 邻居
      - show ipv6 ospf [process-id] neighbor [neighbor-id] [detail]
      - show ipv6 ospf [process-id] neighbor [interface-type interface-number] [neighbor-id] [detail]
    - 数据库
      - show ipv6 ospf [process-id] database [database-summary]
      - show ipv6 ospf [process-id] database [router] [self-originate]
      - show ipv6 ospf [process-id] database [router] [link-state-id]
      - show ipv6 ospf [process-id] database [router] [area-id] [self-originate]
      - show ipv6 ospf [process-id] database [network] [link-state-id]
      - show ipv6 ospf [process-id] database [inter-area-prefix] [link-state-id]
      - show ipv6 ospf [process-id] database [inter-area-router] [link-state-id]
      - show ipv6 ospf [process-id] database [external] [link-state-id]
      - show ipv6 ospf [process-id] database [unknown] [link-state-id]
    - 路由
      - show ipv6 ospf [process-id] route
      - show ipv6 ospf [process-id] route [ipv6-prefix/prefix-length] [longer-prefixes]
      - show ipv6 ospf [process-id] route [ipv6-prefix/prefix-length] [summary]
    - 其他
      - show ipv6 ospf [process-id]
      - show ipv6 ospf [process-id] border-routers
      - show ipv6 ospf [process-id] database [database-summary]
      - show ipv6 ospf [process-id] virtual-links

- EIGRP
  - 配置
    - 路由器
      - router eigrp as-number
      - network network-number [wildcard-mask]
      - [no] auto-summary
      - [no] eigrp log-neighbor-changes
      - [no] metric weights tos k1 k2 k3 k4 k5
      - [no] variance multiplier
      - [no] maximum-paths maximum-paths
      - [no] passive-interface {interface-type interface-number | default}
      - [no] distribute-list {access-list-number | access-list-name} {in|out} [interface-type interface-number]
      - [no] offset-list {access-list-number | access-list-name} {in|out} offset [interface-type interface-number]
      - [no] timers active-time {time | disabled}
    - 接口
      - [no] ip hello-interval eigrp as-number seconds
      - [no] ip hold-time eigrp as-number seconds
      - [no] ip split-horizon eigrp as-number
      - [no] ip summary-address eigrp as-number ip-address mask [admin-distance]
      - [no] ip bandwidth-percent eigrp as-number percent
      - [no] ip authentication mode eigrp as-number md5
      - [no] ip authentication key-chain eigrp as-number name
  - 显示
    - 接口
      - show ip eigrp interfaces [interface-type interface-number] [as-number]
      - show ip eigrp interfaces detail [interface-type interface-number] [as-number]
    - 邻居
      - show ip eigrp neighbors [interface-type interface-number] [as-number]
      - show ip eigrp neighbors detail [interface-type interface-number] [as-number]
    - 拓扑
      - show ip eigrp topology [as-number] [ip-address mask]
      - show ip eigrp topology [as-number] [active|all-links|pending|summary|zero-successors]
      - show ip eigrp topology [as-number] [ip-address mask] [active|all-links|pending|summary|zero-successors]
      - show ip eigrp topology [as-number] [ip-address mask] [detail]
    - 流量
      - show ip eigrp traffic [as-number]
    - 其他
      - show ip eigrp events [starting-event-number ending-event-number] [type]
      - show ip eigrp interfaces [interface-type interface-number] [as-number]
      - show ip eigrp neighbors [interface-type interface-number] [as-number]
      - show ip eigrp topology [as-number] [ip-address mask]
      - show ip eigrp traffic [as-number]

