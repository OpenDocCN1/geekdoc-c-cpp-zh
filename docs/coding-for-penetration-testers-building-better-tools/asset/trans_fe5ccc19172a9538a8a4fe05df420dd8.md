

在 IP 信息中并创建一个 ICMP 数据包。让我们来调查这个过程：

```
>>> ICMP(.default_fields('gw': '0.0.0.0', 'code': 0, 'ts_ori': 67348484, 'addr_mask': '0.0.0.0', 'seq': 0, 'ptr': 0, 'unused': 0, 'ts_rx': 67348484, 'chksum': None, 'reserved': 0, 'ts_tx': 67348484, 'type': 8, 'id': 0)
>>> myicmp = IP(dst='192.168.1.1')/ICMP(type=echo-request)
>>> myicmp
<IP frag=0 proto=icmp dst=192.168.1.1 |ICMP type=echo-request>
>>> ans = srl(myicmp)
Begin emission:
*Finished to send 1 packets.
Received 2 packets, got 1 answers, remaining 0 packets
>>> ans
<IP version=4L ihl=5L tos=0x0 len=28 id=31204 flags=0L ttl=64 proto=icmp chksum=0x7d42 src=192.168.1.1 dst=192.168.1.105 options=[] |ICMP type=echo-reply code=0 chksum=0xffff id=0x0
load='\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00'>
```

首先，我们需要知道 ICMP 层包含哪些字段，因此我们调用了 `default_fields` 方法。现在我们已经知道了 IP 和 ICMP 需要的字段，就可以通过在层类型的构造函数中指定我们想要的值，来创建一个包含这两个层的数据包。在这种情况下，我们正在 ping 我们的网关（192.168.1.1），并且想使用 echo-request（请求请求）ICMP 数据包，这样网关就会向我们返回响应。我们使用斜杠符号来创建数据包：每个层由一个符号隔开。为了验证我们的数据包是否组装正确，我们打印数据包并发现 IP 层和 ICMP 层看起来都是正确的。接下来，我们需要发送该数据包。使用 `srl` 方法，我们需要 Scapy 来发送我们的数据包，它只会接收一个答案。如果我们预期有多个答案，我们将将使用 `sr` 函数。`srl` 函数返回响应数据包。查看我们的答案，我们可以看到 IP 层、ICMP 结构，以及数据包带有填充（padding）。我们可能想要访问响应数据包中的特定信息：

```
>>> ans
<IP version=4L ihl=5L tos=0x0 len=28 id=31204 flags= frag=0
ttl=64 proto=icmp chksum=0x7d42 src=192.168.1.1 dst=192.168.1.105
options=[] |ICMP type=echo-reply code=0 chksum=0xffff id=0x0
load='\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00|Padding|
>>>
>>> ans['IP'].src
'192.168.1.1'
>>> ans['IP'].dst
'192.168.1.105'
>>> ans['ICMP'].type
0
>>> ans.show()
###[ IP ]###
version=4L
hl=5L
tos=0x0
len=28
id=31204
flags=
frag=0
ttl=64
proto=icmp
chksum=0x7d42
src=192.168.1.1
dst=192.168.1.105
options=[]
###[ ICMP ]###
type=echo-reply
code=0
chksum=0xffff
id=0x0
```

