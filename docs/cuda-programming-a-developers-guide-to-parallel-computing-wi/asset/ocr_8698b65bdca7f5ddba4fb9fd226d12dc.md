# Analyzing the results

With a sample size of 16 K and a source dataset size of 1 MB we see the following results on a mostly sorted list:

```
ID:3 GeForce GTX 460: Test 32 - Selecting 16384 from 1048576 elements using 512 blocks
of 32 threads
Select Sample Time - CPU: 0.19 GPU:0.03
Sort Sample Time - CPU: 2.13 GPU:125.57
Count Bins Time - CPU: 157.59 GPU:17.00
Calc. Bin Idx Time - CPU: 0.03 GPU:0.58
Sort to Bins Time - CPU: 163.81 GPU:16.94
Sort Bins Time - CPU: 72.06 GPU:64.46
Total Time - CPU: 395.81 GPU:224.59
Qsort Time - CPU: 185.41 GPU:N/A
```

```
ID:3 GeForce GTX 460: Test 32 - Selecting 16384 from 1048576 elements using 256 blocks
of 64 threads
Select Sample Time - CPU: 0.53 GPU:0.03
Sort Sample Time - CPU: 2.06 GPU:125.57
Count Bins Time - CPU: 157.75 GPU:19.07
Calc. Bin Idx Time - CPU: 0.13 GPU:0.26
Sort to Bins Time - CPU: 164.09 GPU:19.09
Sort Bins Time - CPU: 72.31 GPU:62.11
Total Time - CPU: 396.88 GPU:226.13
Qsort Time - CPU: 184.50 GPU:N/A
```

```
ID:3 GeForce GTX 460: Test 32 - Selecting 16384 from 1048576 elements using 128 blocks
of 128 threads
Select Sample Time - CPU: 0.28 GPU:0.03
Sort Sample Time - CPU: 2.09 GPU:125.57
Count Bins Time - CPU: 157.91 GPU:13.96
Calc. Bin Idx Time - CPU: 0.09 GPU:0.26
Sort to Bins Time - CPU: 164.22 GPU:14.00
Sort Bins Time - CPU: 71.19 GPU:91.33
Total Time - CPU: 395.78 GPU:245.16
Qsort Time - CPU: 185.19 GPU:N/A
```

```
ID:3 GeForce GTX 460: Test 32 - Selecting 16384 from 1048576 elements using 64 blocks of
256 threads
Select Sample Time - CPU: 0.22 GPU:0.03
Sort Sample Time - CPU: 2.00 GPU:125.57
Count Bins Time - CPU: 158.78 GPU:12.43
Calc. Bin Idx Time - CPU: 0.13 GPU:0.49
Sort to Bins Time - CPU: 164.38 GPU:12.39
Sort Bins Time - CPU: 71.16 GPU:84.89
Total Time - CPU: 396.66 GPU:235.80
Qsort Time - CPU: 186.13 GPU:N/A
```