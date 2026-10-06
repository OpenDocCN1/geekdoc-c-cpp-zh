in the IP information and create an ICMP packet. Let's investigate the process:

```
>>> ICMP(.default_fields('gw': '0.0.0.0', 'code': 0, 'ts_ori': 67348484, 'addr_mask': '0.0.0.0', 'seq': 0, 'ptr': 0, 'unused': 0, 'ts_rx': 67348484, 'chksum': None, 'reserved': 0, 'ts_tx': 67348484, 'type': 8, 'id': 0)
>>> myicmp = IP(dst=192.168.1.1')/ICMP(type=echo-request)
>>> myicmp
<IP frag=0 proto=icmp dst=192.168.1.1 |ICMP type=echo-request>
>>> ans = srl(myicmp)
Begin emission:
*Finished to send 1 packets.
Received 2 packets, got 1 answers, remaining 0 packets
>>> ans
<IP version=4L ihl=5L tos=0x0 len=28 id=31204 flags=0L ttl=64 proto=icmp chksum=0x7d42 src=192.168.1.1 dst=192.168.105 options=[] |ICMP type=echo-reply code=0 chksum=0xffff id=0x0
load='\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00'>
```

To begin with, we need to know what fields the ICMP layer has, so we issue the default_fields method. Now that we know what we need for IP and ICMP, we can create a packet with both layers by specifying the values we want in the constructors for the layer types. In this case, we are pinging our gateway (192.168.1.1) and we want to use an echo-request ICMP packet so that the gateway will send us back a response. We create the packet using slash notation: Each layer is separated by a symbol. To verify that our packet is assembled correctly, we print the packet and see that both the IP and the ICMP layers look correct. Next, we need to send the packet. Using the srl method, we need to Scapy to send our packet and it will receive only one answer. If we expected more than one answer, we would use the sr function. The srl function returns the response packet. Looking at our answer, we can see the IP layer, the ICMP structure, and that the packet had padding. We may want to access specific information in the answer packet:

```
>>> ans
<IP version=4L ihl=5L tos=0x0 len=28 id=31204 flags= frag=0
```