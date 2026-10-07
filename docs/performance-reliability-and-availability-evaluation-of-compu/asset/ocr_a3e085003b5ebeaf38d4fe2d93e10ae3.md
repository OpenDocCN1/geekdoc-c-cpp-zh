# Workload Characterization

# $F_{Ed}(u)$

![](bbox=[0.225, 0.116, 0.79, 0.342])

**Figure 24.6** Empirical Cumulative Distribution Function.

The time measured for carrying out the eighty-one Linpack executions was estimated by subtracting the instant of the last measured (3h 14min 50s) from the time instant when the first detected execution (3h 12min 58s). This measured delay $T = 112s$. This information is obtained from Table 24.9. Therefore, the system throughput$^3$ (see Chapter 8) for this workload

```
$X0 = \frac{C0}{T} = \frac{81 executions}{112s} = 0.7232eps.$
```

Using the demand law (see Section 8.3), we may estimate the time demanded from the processor for one execution of the Linpack benchmark by

```
$D_{CPU} = \frac{U_{CPU}}{X0} = \frac{0.44965}{0.7232eps} = 686.51ms.$
```

At the end of scriptlinpack execution, the execution script is stored in the text file Linpack_result.txt. Details on what process were depicted when we described the Linpack benchmark. In that case, Table 24.11 shows the durations of each scriptlinpack execution, totaling eighty-one durations.

# Linpack Results

Factor Solve Total MFLOPS Unit Cray-Ratio

0.876013 0.002379 0.0878392 761.239477 0.002627 15.685571

> $3eps$ stands for executions per second.