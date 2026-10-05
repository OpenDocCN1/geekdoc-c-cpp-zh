# Chapter 6. Special Topic: Networks and Message Passing

| | |
|---| RDMA write latency | 1.83 $\mu secs$ |
| RDMA read latency | 3.42 $\mu secs$ |
| RDMA write bandwidth | 6.24 GB/s |
| RDMA read bandwidth | 6.16 GB/s |

Table 6.1: Latency and bandwidth of bidirectional data transfer between two hosts on a QDR Infiniband network.

the sender. When the sender receives the request packet, it responds by initiating the data transfer. Like RDMA write, RDMA read is completely sided. Once the receiver acquires a remote address key, it posts a work request, but no work request is posted by the sender.The responder, which in this case is the sender, transfers data from its DRAM memory to its host channel adapter without intervention of a processor or the operating system.

# Infiniband latency and bandwidth

Linux Infiniband installation provides commands for measuring network latency and bandwidth. Measurements carried out with the commands

```
ib_write_lat, ib_read_lat, ib_write_bw, ib_read_bw
```

are reported in table 6.1. The measurements are between two nodes. The latencies depend on the distance between the two hosts on the Infiniband network.
Both RDMA read and write have excellent point-to-point bandwidth of 6.2 GB/s. The realized bandwidth is in excess of the advertised maximum of 40 Gbps or 5 GB/s for QDR Infiniband. Interestingly, bandwidths above 6 GB/s are realized between MPI processes as well.
The RDMA read latency is nearly twice the RDMA write latency. We will look more closely at RDMA write and RDMA read to attempt to explain this phenomenon. The microsecond latencies of table 6.1 are impressive. The overhead of a simple spinlock can be a few microseconds. Infiniband network latencies are only about a factor of 10 greater than latencies to DRAM.

> ^7RDMA read requests may be posted to the send queue using ibv_post_send(), just like RDMA write requests.