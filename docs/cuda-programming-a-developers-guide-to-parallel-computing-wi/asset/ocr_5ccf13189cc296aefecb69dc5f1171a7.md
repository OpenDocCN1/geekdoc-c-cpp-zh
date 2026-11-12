| Device/Sample | 256 | 512 | 1024 | 2048 | 4096 | 8192 | 16K | 32K | 64K | 128K | 256K |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Qsort | 337 | 337 | 337 | 337 | 337 | 337 | 337 | 337 | 337 | 337 | 337 |
| GTX460 | 735 | 470 | 235 | 139 | 92 | 91 | 75 | 73 | 81 | 108 | 178 |
| GTX470 | 831 | 535 | 263 | 156 | 97 | 70 | 77 | 68 | 67 | 90 | 155 |
| GTX260 | 1311 | 919 | 463 | 255 | 170 | 124 | 106 | 100 | 106 | 123 | 160 |

![](bbox=[0.18, 0.3, 0.8, 0.53])

FIGURE 6.27 Chart of sample sort on random data.

# Answers on global memory

+   1. Sample sort is quicker when using a mostly sorted list because the thread divergence is significantly less. Each bin has almost the same number of values. We end up with a near-optimal distribution of work to each of the SMs providing there are enough samples chosen from the dataset to generate a reasonable number of blocks.

+   2. One of the key issues of the algorithm is the noncoalesced access to global memory during the radix sort. This is caused by doing an in-place sort using the prefix calculation and the lower and upper bounds for each block. If you instead split each sample set so that it was interleaved by the number of threads, as was the radix sort in the shared memory example, we'd get coalesced access for most of the sort. The drawback of this is potentially wasted memory since some lists are a few entries long and others can be hundreds of entries long.

The other obvious solution is to improve sorting of the samples. At 128 K samples, the sorting of sample data is contributing 43% of the total sort time. However, in practice, we'd never want to use so many samples, and the 32 K results are a more realistic use case. At this point sorting the samples contributes just 7% (see Table 6.16). The largest contributors are sorting the bins (62%), sorting to the bins (14%), and counting the bins (14%). The radix sort is clearly the place to start.