
| Thread 0 | Thread 1 | Thread 2 | Thread 3 | Thread 4 | Thread 5 | Thread 6 | Thread 7 | Thread 8 | Thread 9 | Thread 10 | Thread 11 | Thread 12 | Thread 13 | Thread 14 | Thread 15 | Thread 16 | Thread 17 | Thread 18 | Thread 19 | Thread 20 | Thread 21 | Thread 22 | Thread 23 | Thread 24 | Thread 25 | Thread 26 | Thread 27 | Thread 28 | Thread 29 | Thread 30 | Thread 31 |
| Bank 0 | Bank 1 | Bank 2 | Bank 3 | Bank 4 | Bank 5 | Bank 6 | Bank 7 | Bank 8 | Bank 9 | Bank 10 | Bank 11 | Bank 12 | Bank 13 | Bank 14 | Bank 15 | Bank 16 | Bank 17 | Bank 18 | Bank 19 | Bank 20 | Bank 21 | Bank 22 | Bank 23 | Bank 24 | Bank 25 | Bank 26 | Bank 27 | Bank 28 | Bank 29 | Bank 30 | Bank 31 |

FIGURE 5-3

| Thread 0 | Thread 1 | Thread 2 | Thread 3 | Thread 4 | Thread 5 | Thread 6 | Thread 7 | Thread 8 | Thread 9 | Thread 10 | Thread 11 | Thread 12 | Thread 13 | Thread 14 | Thread 15 | Thread 16 | Thread 17 | Thread 18 | Thread 19 | Thread 20 | Thread 21 | Thread 22 | Thread 23 | Thread 24 | Thread 25 | Thread 26 | Thread 27 | Thread 28 | Thread 29 | Thread 30 | Thread 31 |
| Bank 0 | Bank 1 | Bank 2 | Bank 3 | Bank 4 | Bank 5 | Bank 6 | Bank 7 | Bank 8 | Bank 9 | Bank 10 | Bank 11 | Bank 12 | Bank 13 | Bank 14 | Bank 15 | Bank 16 | Bank 17 | Bank 18 | Bank 19 | Bank 20 | Bank 21 | Bank 22 | Bank 23 | Bank 24 | Bank 25 | Bank 26 | Bank 27 | Bank 28 | Bank 29 | Bank 30 | Bank 31 |

FIGURE 5-4

# Access Mode

Shared memory bank width defines shared memory addresses are in which shared memory banks. Memory bank width varies for devices depending on compute capability. There are two different widths:

- 4 bytes (32-bits) for devices of compute capability 2.x
- 8 bytes (64-bits) for devices of compute capability 3.x

For a Fermi, the bank width is 32-bits and there are 32 banks. Each bank has a bandwidth of 32 bits per two clock cycles. Successive 32-bit words map to successive banks. Hence, the mapping from shared address to bank index can be calculated as follows:

bank index = (address + 4 bytes/bank) % 32 banks

The byte address is divided by 4 to convert to a 4-byte word, and the modulo 32 operation converts the 4-byte word into a bank index. The top of Figure 5-5 illustrates the mapping from byte address to word index for Fermi devices. At the bottom, the mapping from word index to bank index is shown. Note that bank memory wraps around every 32 words. Neighboring words are classified in different banks to maximize the number of possible concurrent accesses for a warp.

| Byte address | 0 | 4 | 8 | 12 | 16 | 20 | 24 | 28 | 32 | 36 | 40 | 44 | 48 | 52 | 56 | 60 |
| 4-byte word index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 |
| Bank index | Bank 0 | Bank 1 | Bank 2 | Bank 3 | Bank 4 | Bank 5 | Bank 6 | Bank 7 | Bank 8 | Bank 9 | Bank 10 | Bank 11 | Bank 28 | Bank 29 | Bank 30 | Bank 31 |
| 4-byte word index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | | 28 | 29 | 30 | 31 |
| 32 | 33 | 34 | 35 | 36 | 37 | 38 | 39 | 40 | 41 | 42 | 43 | | 60 | 61 | 62 | 63 |
| 64 | 65 | 66 | 67 | 68 | 69 | 70 | 71 | 72 | 73 | 74 | 75 | | 92 | 93 | 94 | 95 |
| 96 | 97 | 98 | 99 | 100 | 101 | 102 | 103 | 104 | 105 | 106 | 107 | | 124 | 125 | 126 | 127 |

FIGURE 5-5

A bank conflict does not occur when two threads from the same warp access the same address. In that case, for reads, the word is broadcast to all threads, and for writes, the word is written by only one of the threads which thread performs the write. For Kepler devices, shared memory has 32 banks with the following two modes:

- 64-bit mode
- 32-bit mode

In 64-bit mode, successive 64-bit words map to successive banks. Each bank has a bandwidth of 64 bits per clock cycle. The mapping from shared memory address to bank index can be calculated as follows:

bank index = (byte address + 8 bytes/bank) % 32 banks

A shared memory request from a warp does not generate a bank conflict if two threads access any subword within the same 64-bit word because only a single 64-bit read is necessary to satisfy both requests. As a result, 64-bit mode always causes the same or fewer conflicts for the same access pattern relative to Fermi. However, because Kepler has a bandwidth of 64 bits per clock cycle, accessing 32-bit words in the same bank does not require a retry. It may read 64 bits in a single clock cycle and pass only the 32 bits to each thread. Figure 5-6 illustrates the mapping from byte address to bank index for 32-bit mode. The top figure is shared memory labeled with byte addresses and 4-byte word indices. The bottom figure shows the mapping from 4-byte indices to bank indices. Though word 0 and word 32 are both in bank 0, reading both in the same memory request would not imply a bank conflict.

| Byte address | 0 | 4 | 8 | 12 | 16 | 20 | 24 | 28 | 32 | 36 | 40 | 44 | 48 | 52 | 56 | 60 |
| 4-byte word index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 |
| Bank index | Bank 0 | Bank 1 | Bank 2 | Bank 3 | Bank 4 | Bank 5 | | Bank 30 | Bank 31 |
| 4-byte word index | 0 | 32 | 1 | 33 | 2 | 34 | 35 | 4 | 36 | 5 | 37 | | 28 | 62 | 31 | 63 |
| | 64 | 96 | 95 | 97 | 66 | 98 | 67 | 99 | 68 | 100 | 109 | | 94 | 126 | 95 | 127 |
| | 128 | 160 | | | | | | | | |
| | 192 | 224 | | | | | | | | |

FIGURE 5-6

Figure 5-7 illustrates one case of conflict-free access in 64-bit mode, where each thread accesses different banks. Figure 5-8 illustrates another case of conflict-free access in 64-bit mode, where two threads access the same bank within the same 8-byte word. Figure 5-9 illustrates a two-way bank conflict where two threads access the same bank, but the addresses fall in two different 8-byte words. Figure 5-10 illustrates a three-way bank conflict, where three threads access the same bank and the addresses fall in three different 8-byte words.

# Memory Padding

Memory padding is one way to avoid bank conflicts. A simple case: Suppose you have only five shared memory banks. If all threads access different locations, one way to resolve this is to add padding every *N* elements, where *N* is the number of banks. This shifts the data across banks, as illustrated on the right side of Figure 5-11. The padded memory is never used for storage. Its sole function is to shift data so that data that originated in the same bank are distributed among banks. As a result, the total amount of useful shared memory available to a thread block will decrease.

While Fermi and Kepler have 32 banks, their bank widths differ. You must be careful when padding shared memory on these architectures. Some memory padding patterns in Fermi might lead to bank conflicts in Kepler.

| Bank 0 | Bank 1 | Bank 2 | Bank 3 | Bank 4 | Bank 5 | | Bank 30 | Bank 31 |
|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 | | | |
| 32 | 33 | 34 | 35 | 36 | 37 | | | |
| 64 | 65 | 66 | 67 | 68 | 69 | | | |
| 96 | 97 | 98 | 99 | 100 | 101 | | | |
| 128 | 129 | 130 | 131 | 132 | 133 | | | |
| 160 | 161 | 162 | 163 | 164 | 165 | | | |
| 192 | 193 | 194 | 195 | 196 | 197 | | | |

| Bank 0 | Bank 1 | Bank 2 | Bank 3 | Bank 4 | Bank 5 | | Bank 30 | Bank 31 |
|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 | | | |
| 32 | 33 | 34 | 35 | 36 | 37 | | | |
| 64 | 95 | 66 | 67 | 68 | 69 | | | |
| 96 | 97 | 98 | 99 | 100 | 101 | | | |
| 128 | 129 | 130 | 131 | 132 | 133 | | | |
| 160 | 161 | 162 | 163 | 164 | 165 | | | |
| 192 | 193 | 194 | 195 | 196 | 197 | | | |

FIGURE 5-11

# Access Mode Configuration

Recall that Kepler devices support 4-byte and 8-byte shared memory access modes. The default is 4-byte mode. The access mode can be queried using the following runtime API:

```
cudaError_t cudaDeviceGetSharedConfig(cudaSharedMemConfig *pConfig);
```

The result is returned in pConfig. The returned bank configuration can be either of the following values:

```
cudaSharedMemBankSizeFourByte
cudaSharedMemBankSizeEightByte
```

You can use the following function to set a new bank size on devices with configurable shared memory banks:

```
cudaError_t cudaDeviceSetSharedMemConfig(cudaSharedMemConfig config);
```

The supported bank configurations are:

```
cudaSharedMemBankSizeDefault
cudaSharedMemBankSizeFourByte
cudaSharedMemBankSizeEightByte
```

Changing the shared memory configuration between kernels might require an implicit device synchronization point. Changing the shared bank size will not increase shared memory usage or occupancy of kernels, but it may have a major effect on performance. A large bank size may yield higher bandwidth for shared memory, but may result in bank conflicts depending on the application's shared memory access patterns.

# Configuring the Amount of Shared Memory

Each SM has 64 KB of on-chip memory. The shared memory and L1 cache share this hardware resource. CUDA provides two methods for configuring the size of L1 cache and shared memory:

- Per-device configuration
- Per-kernel configuration

You can configure how much L1 cache and how much shared memory will be used by kernels launched on a device using the following runtime function:

```
cudaError_t cudaDeviceSetCacheConfig(cudaFuncCache cacheConfig);
```
