```
C[i + blockDim.x] = A[k + blockDim.x];
[i + 2 * blockDim.x] = A[k + 2 * blockDim.x] + B[2 * blockDim.x];
[i + 3 * blockDim.x] = A[k + 3 * blockDim.x] + B[k + 3 * blockDim.x];
```

You can download the source in readSegmentUnroll.cu from Wrox.com. Compile it with L1 cache (-Xptxas -dlcm=ca) and run the following tests:

```
$ /readSegmentUnroll 0
warmup      << 32768, 512 >>> offset      0 0.001990 sec
unroll      << 8192, 512 >>> offset      0 0.000599 sec
$ /readSegmentUnroll 1
warmup      << 32768, 512 >>> offset      11 0.002214 sec
unroll      << 8192, 512 >>> offset      11 0.000615 sec
$ /readSegmentUnroll 2
warmup      << 32768, 512 >>> offset      128 0.001989 sec
unroll      << 8192, 512 >>> offset      128 0.000598 sec
```

Surprised? This unrolling has a tremendous impact on performance, even when address alignment matters. Relative to the original readSegmentExample with no unrolling, test runs demonstrate 3.04 and 3.11 times faster. With an I/O-bound kernel, it seems that exposing sufficient memory access parallelism is a high priority. As we expected, the two test cases still outperform the case where accesses are misaligned.

However, unrolling does not affect the number of memory operations performed (only the number concurrently-in-flight). You can confirm this by measuring load and store efficiency metrics of both the original and unrolled kernels using the following command to test the misaligned case (offset=11).

Sample results are summarized below. The load and store efficiency are the same for the two kernels.

```
readOffset      gid_efficiency 49.69%
readOffset      gst_efficiency 100.00%
readOffsetUnroll4 gid_efficiency 50.79%
readOffsetUnroll4 gst_efficiency 100.00%
```

Now, try measuring the number of load and store transactions in the misaligned case (offset=11).

```
$ nvprof --deves 0 --metrics load_transactions,gst_transactions
  ./readSegmentUnroll 11
```

Sample results are summarized below. The number of read/write transactions performed by the unrolled kernel is significantly reduced.

```
readOffset      gid_transactions 123284
readOffset      gst_transactions 32928
readOffsetUnroll4 gid_transactions 33152
readOffsetUnroll4 gst_transactions 8064
```

# Exposing More Parallelism

To expose sufficient parallelism, you should experiment with the grid and block size of a kernel to find the best execution configuration for that kernel. Run the following tests to experiment with block size for properly aligned memory accesses (offset=0). Note that you will