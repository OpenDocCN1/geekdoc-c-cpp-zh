# Fault Injection and Failure Monitoring

Table 26.3 Transitions’ Attributes

| Transition | Guard | $\pi$ (Priority) | $\omega$ (Weight) | $\lambda$ (Rate) |
|---|---|---|---||
| F1 | | 1 | | $\hat{\lambda}_{F1}$ |
| R1 | #OSD = 0 | 1 | | $\mu_{R1}$ |
| F2 | | 1 | | $\hat{\lambda}_{F2}$ |
| R2 | #OSD = 0 | 1 | | $\mu_{R2}$ |
| OSF1 | | 1 | 1 | |
| OSF2 | | 1 | 1 | |
| OSF | | 1 | | $\hat{\lambda}_{OS}$ |
| OSR | #HWD = 0 | 1 | | $\mu_{OS}$ |
| OSF1 | | 1 | 1 | |
| HWF | | 1 | | $\hat{\lambda}_{HW}$ |
| HWR | | 1 | | $\mu_{HW}$ |
| STF | | 1 | | $\hat{\lambda}_{ST}$ |
| STR | | 1 | | $\mu_{ST}$ |

# EXERCISES

**Exercise 1.** What are the aims for using fault injection?

**Exercise 2.** Explain what are **a)** hardware-based, **b)** software-based, and **c)** hardware-software-based fault injectors?

**Exercise 3.** Software-based fault injectors may be employed **a)** to inject actual soft-wares in a system, **b)** to emulate hardware faults, and **c)** to simulate hardware and software faults in the models. Explain each of these mechanisms.

**Exercise 4.** What do you understand by an invasive or a non-invasive fault injection mechanism? Give examples.

**Exercise 5.** Explain the purpose of the fault acceleration mechanisms and where these mechanisms are usually applied.

**Exercise 6.** What are failure scaling factors? Explain.

**Exercise 7.** Consider a stress experiment was carried out, and a sample of two hundred $TTFs$ was collected. The $MTTF$ calculated from the sample was $MTTF=246.3$, (a) if the compression factor is constant and equal to $CF = 1/8$, what is the mean time to failure at normal operation conditions? (b) if the probability distribution function of the $TTF$ is exponentially distributed, present the $CDF$ and the cumulative hazard function at normal conditions.