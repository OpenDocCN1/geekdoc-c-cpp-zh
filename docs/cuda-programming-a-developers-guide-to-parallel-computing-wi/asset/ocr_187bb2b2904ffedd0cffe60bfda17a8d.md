```
33554432 2663.6

Device to Host Bandwidth, 1 Device(s), Pinned memory
Transfer Size (Bytes) Bandwidth(MB/s)
33554432 3225.8

Device to Device Bandwidth, 1 Device(s)
Transfer Size (Bytes) Bandwidth(MB/s)
33554432 113232.3
```

One of the things you'll see when using this example program is just how much benefit using pinned memory on your system brings. We looked at this in Chapter 9, but there is nothing like seeing it on your own system to drive home the point that pinned memory can be much faster for memory transfers. Even a modern Sandybridge-E processor achieves 3 GB/s versus 2.3 GB/s when using pinned versus paged memory on a similar PCI-E 2.0 x8 link.

Typical memory on a consumer GPU card is anything from 512 MB (88/9800 series) to 2 GB (GTX680). There is really no reason why you should not pin system memory to do the transfers to or from the GPU. Even in a 32-bit system with a 4 GB memory limit, CUDA will still be using pinned transfers in the background. Therefore, you may just as well pin the memory yourself and avoid the implicit pagable to pinned memory copy within the driver.

As memory is now very cheap there is no reason why you should not fully load the machine. This is especially the case if you have more than one GPU card or are using Tesla cards. You can purchase 16 GB of host memory for less than 100 euros/dollars/pounds.

If we take the memory clock from the GTX470, there is 1674 MHz with a bus width of 320 bits. Thus, we take the bus width and divide by 8 to get bytes (40 bytes). Next we multiply this by the clock rate (66,960 MB/s). Then we multiply by 2 for GDDR5 (133,920 MB/s). Then we divide by 1000 to get listed memory bandwidth (133.9 GB/s) or 1024 (130.8 GB/s) to get actual bandwidth.

So why do we get device-to-device bandwidth of 113,232 MB/s instead of 133,920 MB/s? Where did the missing 20 MB/s or 15% of the memory bandwidth go? The GPU never achieves this theoretical peak bandwidth. This is why it's useful to run the bandwidth test as opposed to calculating the theoretical peak. You then have a very good idea of what bandwidth you will get in your system, with your PCI-E arrangement, your host CPU, your CPU chipset, your host memory, etc. By knowing this you know what your application should be able to achieve on a given target and can therefore see how much potential you have yet to exploit.

Note with Tesla-based Fermi devices you can gain a significant boost in bandwidth by disabling the ECC memory option using the nvidia-smi tool. Error checking and correction (ECC) distributes the bit patterns using Hamming codes. This, in effect, means you need a larger memory space to store the same data block. This additional storage requirement means you trade both space and speed for the extra redundancy ECC brings. NVIDIA claims to have addressed this issue in Kepler K20 (GK110), where the impact of using ECC is claimed to be around one-third of that of Fermi.

# SimpleP2P

The SimpleP2P example shows how to use the P2P memory transfer capabilities introduced in compute 2.x devices (Fermi). The principle of P2P transfers to avoid having to go through host