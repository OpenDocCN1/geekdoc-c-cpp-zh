# Workload Characterization

Table 24.7

# Livermore Loops - Execution Time (s) - Sample Size = 100.

| | | | | | | | | | |
|---|---|---|---|---|---|---|---|---||
| 1.6475 | 1.7330 | 1.9164 | 1.6553 | 1.6220 | 1.7002 | 1.6535 | 1.6623 | 1.6750 | 2.0213 |
| 1.6772 | 2.0070 | 1.9102 | 1.6333 | 1.6116 | 1.6100 | 1.6926 | 1.6216 | 1.7082 | 1.8907 |
| 1.6362 | 1.9237 | 1.8715 | 1.8311 | 1.8270 | 1.6585 | 1.6180 | 1.6073 | 1.7872 | 1.8362 |
| 1.6887 | 1.9181 | 1.8271 | 1.6549 | 1.7110 | 1.6209 | 1.6187 | 1.6733 | 1.8434 | 2.1401 |
| 1.6761 | 2.2834 | 1.8616 | 1.7737 | 1.6120 | 1.8410 | 1.6998 | 1.6728 | 1.7011 | 1.9049 |
| 1.6253 | 2.2834 | 1.7739 | 1.6104 | 1.6394 | 2.0386 | 1.0660 | 1.6117 | 2.0276 | 1.8762 |
| 1.6222 | 1.9232 | 1.9019 | 1.6771 | 1.6431 | 1.8624 | 1.7094 | 1.6396 | 1.6811 | 1.9521 |
| 1.7626 | 2.1220 | 1.9437 | 1.6726 | 1.6272 | 1.6153 | 1.6821 | 1.6784 | 1.6821 | 1.8233 |
| 1.6307 | 1.9951 | 1.8822 | 1.6288 | 1.6197 | 1.8011 | 1.7038 | 1.6581 | 1.6482 | 1.6694 |
| 1.6252 | 2.0549 | 1.6760 | 1.6814 | 1.6707 | 1.6963 | 1.6290 | 1.6249 | 1.6857 | 1.6559 |

Table 24.8

# Statistical Summary - Execution Time (s) - Livermore Loops

| Mean | SD | Var | CoV (%) | Min | Q1 | Med |
|---|---|---|---|---|---|---||
| Execution Time (s) | 1.7431 | 0.0165 | 0.0261 | 9.26 | 1.0600 | 1.6338 | 1.6813 |
| Q3 | Max | Range | IIQ | Skewness | Kurtosis |
| Execution Time (s) | 1.8428 | 2.2834 | 1.2234 | 0.2091 | 0.27 | 3.35 |

The confidence interval of the mean execution time (met) with 95% degree of confidence was calculated using the nonparametric bootstrap. The confidence interval estimated

> met ∈ (1.7109s, 1.7725s).

# Dhrystone

The Dhrystone benchmark was implemented by Reinhold P. Wecker and published in 1984 using a subset of the ADA program language (the Pascal subset of ADA) [459]. Later on, it was translated to PASCAL, Fortran, and C. Among all these implementations, the C implementation is the most popular [317]. Dhrystone consists of 12 procedures included in one measurement with 94 states; during one loop (one Dhrystone), 101 tests (103 in the C version) are executed dynamically on integer instruction performance focusing on integer instruction performance since, in that, many computers used integer instruction, and the Whestone benchmark already focused on floating-point instruction. The basis for the Dhrystone benchmark was a literature survey on the distribution of source language features, taking into account non-numeric, system-type