
## 7.2. Offload

```
hostmic_scale(v+shft, len);
sum[mc] = hostmic_sum(v+shft, len);
}
```

```c
printf(" nmic = %d\n", nmic);
/*
 * wait for mics to get back
*/
for(int mc=0; mc < nmic; mc++) {
#pragma offload_wait target(mic:mc) wait(1)
}
```

```c
/*
 * free mem on mic devices
*/
for(int mc=0; mc < nmic; mc++) {
long shft = mc*n/nmic;
long len = (mc+1)*n/nmic - mc*n/nmic;
#pragma offload_transfer target(mic:mc) [shft:len]:
nocopy(v[shft]:align(G4)) alloc_if(0) free_if(1)
}
double ans = 0;
for(int mc=0; mc < nmic; mc++) {
    ans += sum[mc];
}
printf(" leibniz4: sum = %e\n", ans);
```

```c
_mm_free(v);
mic_exit();
```

Notice that the first argument to hostmic_scale() and hostmic_sum() is v+shft and not just v. The offload region that scales and sums is preceded by the signal clause. It makes no sense to use blocking offloads if multiple MIC devices are in play.

### 7.2.4 Offload bandwidth

If the Phi/MIC devices are used in offload mode, there is a significant cost to the data transfer between the host and MIC devices. The PCIe bus, which connects the host with the MIC devices (via the chipset; see figure 7.1), has low bandwidth. Its bandwidth is more than an order of magnitude less than the bandwidth to memory of the MIC devices or even the host. Data transfer between the host and the Xeon Phi coprocessors imposes serious limits on the advantages as well as utility of the coprocessor model.

To time the transfers between the host and the MIC devices, we use functions such as the following:

```c
void xfer_in(double *v, long n, int nmic){
long fst[nmic+1];
for(int i=0; i <= nmic; i++)
fst[i] = i*n/nmic;

for(int mc=0; mc < nmic; mc++){
 long shift = fst[mc];
 long len = fst[mc+1] - fst[mc];
#pragma offload target(mic:mc)
in(v[shift:len]:align(64) alloc_if(0) free_if(0)) signal(1)
dummy(v+shift, len);
}

for(int mc=0; mc < nmic; mc++)
#pragma offload_wait target(mic:mc) wait(1)
}
```

This function transfers data into nmic devices. Analogous functions transfer data out of the MIC devices or use the inbuilt clause to transfer data both into the MIC devices during entry to the offload region and out at exit.

| Cycles/Byte (One MIC) | Bandwidth (One MIC) | Cycles/Byte (Two MICs) | Bandwidth (Two MICs) |
|---|---|---|---|---|
| IN | 0.42 | 6.48 GB/s | 0.40 | 6.75 GB/s |
| OUT | 0.42 | 6.48 GB/s | 0.40 | 6.75 GB/s |
| INOUT | 0.81 | 3.24 GB/s | 0.77 | 3.51 GB/s |

Table 7.3: Offload bandwidths in transferring data to one MIC device or simultaneously to two MIC devices. In cycles/byte, the cycles are of the 2.7 GHz AVX host.

Table 7.3 shows that data can be moved into or out of a single MIC device at rate of nearly 7 GB/s. That rate is close to the peak rating of the PCIe bus. bandwidth is nearly halved if data is input to the MIC device during entry to the offload region and output from the MIC device at exit. With the inout clause, data flowing in and data flowing cannot be overlapped.

With simultaneous transfer to two MIC devices, the bandwidths are almost unchanged. The bandwidth cannot be doubled because both devices are on the same bus. Latencies for data transfer are of the order of a millisecond.

**Exercise 7.2.1.** Write a program to find the sum of a long array that outsources parts of the work to each Phi device on the system. Do you expect the program to result in any speedup?

**Exercise 7.2.2.** Write a program that during a single iteration replaces each entry of a 2D array (with periodic boundaries) by the average of its north, south, east, and west entries. The program must outsource parts of the computation to each Phi device on the system. Do you expect a speedup if only a few iterations to be performed? What if the iterations are large?

**Exercise 7.2.3.** Assume that a matrix, whose dimensions you may assume to be suitably large, is split between the host and Phi coprocessors. Write a program that transposes this matrix. Discuss the difficulties that arise because of the heterogeneity between the processor and coprocessors.

## 7.3 Two examples: FFT and matrix multiplication

### 7.3.1 FFT

Section 7.3.1 looks at the Fast Fourier Transform (FFT) implemented inside the MKL library. For small $n$, the FFT on the Phi/MIC device is twice as fast as it is on the AVX. For large $n$ such as $n=2^{26}$, the FFT does not appear to be well optimized and is slower on the Phi/MIC device by more than a factor of 8. The fact that even FFT reaches only 15% of the peak point bandwidth shows how misleading metric can be. To approach the peak bandwidth, FFT is a good basis for comparing the Phi against its AVX host. It is one of the most frequently employed algorithms. Unlike LINPACK benchmark, the cost of memory accesses cannot be completely hidden. The class FFT was employed to time FFTs on the MIC device as well as the host.

```c
__declspec(target(mic))
class FFT {
private:
    DFTI_DESCRIPTOR_HANDLE handle;
public:
    FFT(int n, long count);
    ~FFT();
    void fwd(double*f){
        DftiForward(handle, f);
    }
    void bwd(double*f){
        DftiBackward(handle, f);
    }
};
```

This class, like similar classes discussed in chapter 2, the MKL library. As far the definition of this class is concerned, no new points arise with either MKL or Phi/MIC syntax. Therefore, it is omitted. The FFT class may be used on the host computer, offloaded to the MIC device, or used natively on a MIC device if compiled with the -mic flag. Both forward and backward transforms are in place. The forward transform is suitably normalized.

Table 7.4 shows that the Phi is faster than its host for n = 64 and n = 1,024. The multiple levels of cache found on the host are useful, even for a regular and arithmetic-intensive computation such as FFT. For n = 8,192, the Phi and its host are almost of the same speed. For n = $8,192^2 = 2^{26}$, MKL’s FFT is not optimized on either platform, but the host is much better.

If a large number of FFTs are to be computed, we may ask, does it make sense to offload from the AVX host to the MIC coprocessor? The answer is emphatically no. For n = 8,192, the AVX host takes 0.13 cycles per byte of data (see table 7.4). Table 7.3 shows that sending data to a coprocessor and getting it back will take 0.81 cycles, swamping the cost of the FFT.

Table 7.4 shows that a complex-to-complex FFT of size n = 1,024 takes 0.09 log2 n host cycles (with the AVX host at 2.7 GHz) on the Phi. As shown in chapter 2, the number of arithmetic operations in a single complex FFT of dimension n, with a power of 2, may be assumed to be $5logn2 n$. Therefore, the floating point throughput is $5/.09 \times 2.7 = 150 GFLOps/sec$. This floating point throughput is only 15% of the theoretical peak of the Phi.

### 7.3.2 Matrix multiplication

Algorithms that are capable of approaching the theoretical peak are not many. These alg must involve a great number of arithmetic operations relative to the data they access. In addition, their structure must permit hiding the cost of multiple accesses of the same data item. numerical linear algebra is the main source of such algorithms.

The number of arithmetic operations in $C = C + AB$, where $A, B, C$ are $n \times n$ matrices, for large $n$, a great number of arithmetic operations are carried out for every byte is accessed.

| n | AVX | AVX | MIC | MIC |
|---|---|---|---|---|
| Cycles log2 | Cycles/Byte | Cycles log2 | Cycles/Byte |
| 64 | 0.19 | 0.07 | 0.11 | 0.04 |
| 1,024 | 0.17 | 0.11 | 0.09 | 0.06 |
| 8,192 | 0.16 | 0.13 | 0.15 | 0.12 |
| 8,192 × 8,192 | 2.16 | 4.26 | 17.55 | 28.52 |

Table 7.4: Number of cycles consumed by complex FFT of size n. For both the 2.7 GHz AVX host (see table A1 for the full name) and the Phi/MIC coprocessor, the reported numbers are host cycles.

 Xeon Phi instructions

Before taking a closer look at the Phi architecture, we go back to figure 7.2 and summarize a few features of the Phi architecture. Up to four threads can be scheduled to run on every Phi/MIC core. The hardware switches between threads in a single cycle. It prefers round-robin scheduling, and it never executes the same thread in

