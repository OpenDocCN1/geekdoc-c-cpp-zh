| Threads | GTX470 | GTX260 | GTX460 |
|---|---|---|---|
| 1 | 33.27 | 66.32 | 27.47 |
| 2 | 19.21 | 37.53 | 15.87 |
| 4 | 11.82 | 22.29 | 9.83 |
| 8 | 9.31 | 16.24 | 7.88 |
| 16 | 7.41 | 12.52 | 6.36 |
| 32 | 6.63 | 10.95 | 5.75 |
| 64 | 6.52 | 10.72 | 5.71 |
| 128 | 7.06 | 11.63 | 6.29 |
| 256 | 8.61 | 14.88 | 7.82 |

What you can see from Table 6.13 and Figure 6.21 is that 32 threads work quite well, but this is marginally beaten by 64 threads on all the tested devices. It’s likely that having another warp to execute is hiding a small amount of the latency and will also improve slightly the memory bandwidth utilization.

Moving beyond 64 threads slows things down, so if we now fix the number of threads at 64 and increase the dataset size what do we see? See Table 6.14 and Figure 6.22 for the results. In fact we see an almost perfect linear relationship when using a single SM, as we are currently doing.

As Table 6.14 shows, 1024 KB (1 MB) of data takes 1486 ms to sort on the GTX460. This means we can sort 1 MB of data in around 1.5 seconds (1521 ms exactly) and around 40 MB per minute, regardless of the size of the data.

A 1 GB dataset would therefore take around 25–26 minutes to sort, which is not very impressive.

So what is the issue? Well currently we’re using just a single block, which in turn limits us to a single SM. The test GPU’s consists of 14 SMs on the GTX470, 27 SMs on the GTX260, and 7 SMs on the

![](bbox=[0.23, 0.61, 0.77, 0.83])

FIGURE 6.21
Graph of single SM GMEM sort (1K elements).