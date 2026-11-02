![](bbox=[0.18, 0.13, 0.8, 0.48])

Fig. 10. The evolutions of CGA, SCQGA and QIGA

| Parameter | CGA | SCOGA | QIGA |
|---|---|---|---|
| Global time | 73.990 s | 38.599 s | 19.263 s |
| Self time | 2.447 s | 1.417 s | 1.390 s |
| Evaluation time | 59.561 s | 31.536 s | 11.750 s |
| Calls of evaluation function | 25200 | 19200 | 4836 |
| Ratio between evaluation and global time | 80.5 % | 81.7 % | 60.9 % |
| Number of generations | 300 | 300 | 300 |
| Successful runnings in 10 attempts (with fitness of 100%) | 7 | 6 | 6 |

Table 1. A comparison between CGA, SCQGA and IQGA

Unfortunately, the number of successful runs in 300 generations is only in the order of 70% for CGA, and 60% for the rest two algorithms. It occurs due to the constraint that only 100% in fitness evaluation is accepted. In other applications, this constraint may be not critical.

# 6. Conclusion

In this chapter we did a summary outline of GAs and discussed some possible applications. We presented three extrinsic evolutionary designs of digital circuits at gate level using GAs.

Future research must be done in this area. Firstly it is important to find a better representation of the circuit in chromosomes, because complex functions need a great number of architecture bits, which directly influences the GA search space. EHW successfully succeeds only when fitness reaches 100% and in huge search spaces this condition may be not always possible. This is the main reason that for the time being the