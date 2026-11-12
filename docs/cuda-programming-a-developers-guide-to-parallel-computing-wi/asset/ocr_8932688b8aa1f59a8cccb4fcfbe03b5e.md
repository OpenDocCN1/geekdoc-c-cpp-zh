# Table 6.14 GMEM Sort by Size

| | Absolute Time (ms) | | | Time per KB (ms) | | |
|---|---|---|---|---|---|---|
| Size (Kb) | GTX470 | GTX260 | GTX460 | GTX470 | GTX260 | GTX460 |
| 1 | 1.67 | 2.69 | 1.47 | 1.67 | 2.69 | 1.47 |
| 2 | 3.28 | 5.36 | 2.89 | 1.64 | 2.68 | 1.45 |
| 4 | 6.51 | 10.73 | 5.73 | 1.63 | 2.68 | 1.43 |
| 8 | 12.99 | 21.43 | 11.4 | 1.62 | 2.68 | 1.43 |
| 16 | 25.92 | 42.89 | 22.75 | 1.62 | 2.68 | 1.42 |
| 32 | 51.81 | 85.82 | 45.47 | 1.62 | 2.68 | 1.42 |
| 64 | 103.6 | 171.78 | 90.94 | 1.62 | 2.68 | 1.42 |
| 128 | 207.24 | 343.74 | 181.89 | 1.62 | 2.69 | 1.42 |
| 256 | 414.74 | 688.04 | 364.09 | 1.62 | 2.69 | 1.42 |
| 512 | 838.25 | 1377.23 | 737.85 | 1.64 | 2.69 | 1.44 |
| 1024 | 1692.07 | 2756.87 | 1485.94 | 1.65 | 2.69 | 1.45 |

GTX460. Clearly, we're using a small fraction of the real potential of the card. This has been done largely to simplify the solution, so let's look now at using multiple blocks.

The output of one SM is a single linear sorted list. The output of two SMs is therefore two linear sorted lists, which is not what we want. Consider the following dump of output from a two-block version of the sort. The original values are in reverse sorting order from 0x01 to 0x100. The first value shown is the array index, followed by the value at that array index.

![](bbox=[0.2, 0.616, 0.7, 0.85])

# FIGURE 6.22 GMEM graph sorted by size.