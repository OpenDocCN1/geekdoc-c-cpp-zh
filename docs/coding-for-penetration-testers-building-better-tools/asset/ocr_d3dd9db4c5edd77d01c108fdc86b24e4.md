We will call scripts sendICMP.py and receiveICMP.py. The file we are going to transfer to the system is the Netcat binary. This file is /bin/nc.traditional and is 22,076 bytes. Let's determine the number of packets that will be used:

```
root@~#$ ls -l /bin/nc.traditional
-rwxr-xr-x 1 root 22076 Jun 21 2008 /bin/nc.traditional
root@~#$ python -c 'print 22076.0/32.0'
689.875
```

Python is also a handy calculator. We see our file will take 689.8 packets to send. So we round that up to 690 and set up the sniffer to capture our file:

```
root@~#$ python receiveICMP.py mync 192.168.1.1 690
WARNING: No route found for IPv6 destination :: (no default route?)
siffing with filter (icmp and host 192.168.1.1) for 690 bytes
```

Our sniffer is now listening for packets to 192.168.1.1 and will receive 690 packets into the mync file. We see all arguments processed correctly and our sniffer is waiting for input. Now to send our file:

```
root@~#$ python sendICMP.py /bin/nc.traditional 192.168.1.1
WARNING: No route found for IPv6 destination :: (no default route?)
```

Data size is 22076
Data sent

We send our file using sendICMP.py to 192.168.1.1. We see the file has loaded correctly and all the data was sent. Our sniffer should have gotten all the packets and we should now have a copy of our file as mync. Let's verify that the file is the same as our original:

```
root@~#$ python receiveICMP.py mync 192.168.1.1 690
WARNING: No route found for IPv6 destination :: (no default route?)
sning with filter (icmp and host 192.168.1.1) for 690 bytes
Data Received
root@~#$ ls -l /bin/nc.traditional mync
-rwxr-xr-x 1 root 22076 Jun 21 2008 /bin/nc.traditional
-r-r--r-- 1 root 22076 Mar 27 16:53 mync
root@~#$ md5sum /bin/nc.traditional mync
781eb495b27a7aac194efe0b2a7c49 /bin/nc.traditional
781eb495b27a7aac194efe0b2a7c49 mync
```

We can see that our file transferred successfully, and when we