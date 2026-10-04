# 280 COMPUTATIONAL METHODS FOR NGS DATA ANALYSIS

# TABLE 12.2 The Average Value of True Positive Rate of Assemblers with Twofold
Transcript Coverage

| FPKM Complete Coverage | Soapdenovo Fractional Coverage | Trinity Fractional Coverage |
|---|---|---|---|---|---|---|---|n| | Tophat | SplipMap | 90% | 50% | 10% | 90% | 50% | 10% |
| 0.5 | 0.8318 | 0.8166 | 0.0096 | 0.0314 | 0.2194 | 0.0086 | 0.0276 | 0.1905 |
| 1 | 0.7438 | 0.7254 | 0.0095 | 0.0350 | 0.2078 | 0.0086 | 0.0269 | 0.1820 |
| 2 | 0.6413 | 0.6231 | 0.0089 | 0.0276 | 0.1854 | 0.0081 | 0.0246 | 0.1645 |
| 5 | 0.4900 | 0.4746 | 0.0073 | 0.0219 | 0.1462 | 0.0066 | 0.0200 | 0.1349 |
| 10 | 0.3663 | 0.3551 | 0.0056 | 0.0167 | 0.1119 | 0.0052 | 0.0158 | 0.1073 |
| 15 | 0.2912 | 0.2826 | 0.0044 | 0.0135 | 0.0912 | 0.0043 | 0.0132 | 0.0892 |

The identification of transcripts by Trinity and Soapdenovo-Trans are based on fractional method.

# TABLE 12.3 The Average Value of True Positive Rate of Assemblers with Fivefold
Transcript Coverage

| FPKM Complete Coverage | Soapdenovo Fractional Coverage | Trinity Fractional Coverage |
|---|---|---|---|---|---|---|---|n| | Tophat | SplipMap | 90% | 50% | 10% | 90% | 50% | 10% |
| 0.5 | 0.9318 | 0.9100 | 0.0109 | 0.0356 | 0.2466 | 0.0098 | 0.0313 | 0.2137 |
| 1 | 0.7290 | 0.8222 | 0.0101 | 0.0343 | 0.2358 | 0.0097 | 0.0306 | 0.2057 |
| 2 | 0.7295 | 0.7084 | 0.0110 | 0.0314 | 0.2106 | 0.0092 | 0.0279 | 0.1861 |
| 5 | 0.5576 | 0.5402 | 0.0083 | 0.0250 | 0.2160 | 0.0072 | 0.0227 | 0.1529 |
| 10 | 0.4170 | 0.4064 | 0.0160 | 0.0190 | 0.1271 | 0.0060 | 0.0179 | 0.1217 |
| 15 | 0.3316 | 0.3219 | 0.0050 | 0.0154 | 0.1036 | 0.0049 | 0.0150 | 0.1012 |

The identification of transcripts by Trinity and Soapdenovo-Trans are based on fractional method.

We have chosen this as either two or fivefold level of coverage for comparative purposes throughout. The combined results of the true positive rate are given in Tables 12.2 and 12.3 and are shown in Figures 12.4 and 12.5.

The sensitivity or the true positive rate provides only one aspect of the performance metric. We look at the positive transcripts that are common in both the reference-based assemblers and novo assemblers. The results for common transcripts for both and fivefold coverage are given in Tables 12.4 and 12.5 and graphically in Figures 12.6 and 12.7, respectively.

# 12.7 SUMMARY AND CONCLUSION

The Flux simulator generated 100-bp, paired-end RNA-seq data sets with a realistic error model based on Illumina technology as described in the section on Experiment. We have generated five different data sets, each with at least 12 million paired-end reads. Multicore high-performance computers were used to assemble