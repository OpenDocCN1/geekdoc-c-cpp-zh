![](bbox=[0.246, 0.117, 0.781, 0.344])

# FIGURE 11.15

DBThread scaling with 32 KD-trees. Note that each point on the X-axis represents a different combination of <DBThreads, FLANNThread, KD-trees>.

| DB,KD-trees | Xeon Create Time (ms) | XeonSearch Time (ms) | MIC Create Time (ms) | MIC Search Time (ms) |
|---|---:|---:|---:|---:|
| 4,2 | 58 | 103 | 43 | 87 |
| 8,4 | 55 | 72 | 49 | 59 |
| 16,8 | 123 | 56 | 98 | 47 |
| 32,16 | 353 | 27 | 343 | 23 |

# FIGURE 11.16

DBThread scaling with respect to KD-trees comparing Xeon versus Xeon Phi.

![](bbox=[0.183, 0.669, 0.818, 0.865])

# FIGURE 11.17

Impact of vectorization on tree creation and search time.