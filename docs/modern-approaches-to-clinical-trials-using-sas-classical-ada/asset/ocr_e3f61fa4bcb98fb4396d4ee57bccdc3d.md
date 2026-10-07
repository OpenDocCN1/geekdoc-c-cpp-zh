maximum sample size () a multistage design is a function of the maximum information () and a nuisance parameter. a test for the difference between two normally distributed means has $N_{max\Delta}=4s^2/I_{max}$; a test for the difference between two binomial proportions $N_{max}=2((p_T)(1-p_T)+(p_C)(1-p_C))/I$, for treatments T and C.

We replicate an example for a binary endpoint described in Tsiatis [37]. Consider a hypothetical two-arm trial with equal allocation designed to test the efficacy of an experimental new treatment compared to the standard of care (control). We denote $p_T$ as the rate of response in the treatment and $p_C$ as the rate of response in the control arm.

The best guess for the response on the control arm is 0.15. In order to detect a meaningful difference of 0.15 with $p_T=0.30$, 316 subjects are required for 90% power for a one-sided $\alpha=0.025$ classical design. The information required is approximately 468. Partial output from `proc seqdesign` from [Example Code 3.5 Information Based Design - Fixed Sample Size](Example Code 3.5 Information Based Design - Fixed Sample Size) is presented in [Figure 3.1 Output for Example Code 3.5](Figure 3.1 Output for Example Code 3.5).

# Example Code 3.5 Information Based Design - Fixed Sample Size

```
proc seqdesign altref=0.15;
OneSidedFixedSample: design nstages=1
al=upper alpha=0.025 beta=0.10;
samplesize model=twsamplefreq(nullprop=0.15 test=prop);
```

# Figure 3.1 Output for Example Code 3.5

| | Sample Sizes (N) | | |
|---|---|---|---|---|---||
| Fractional N | | Ceiling N |
| | N(Grp 1) | N(Grp 2) | Information | N(Grp 1) | N(Grp 2) |
| | 315.22 | 157.01 | 157.01 | 457.0 | 316 | 158 | 158 | 468.1 |

Alternatively, we design the study with 4 equally-spaced stages using an O 'Brien Fleming-like boundary using the Lan-Deets spending function. To obtain 90% power for a one-sided $\alpha=0.025$ alternative, the information needed is approximately 477, with a maximum sample size of 322. Partial output from `proc seqdesign` in [Example Code 3.6 Information Based Design – 4-Stage Design](Example Code 3.6 Information Based Design – 4-Stage Design) is shown in [Figure 3.2 Sample Size and Maximum Information for 4-Stage Design](Figure 3.2 Sample Size and Maximum Information for 4-Stage Design) and [Figure 3.3 Boundary Information for 4-Stage Design](Figure 3.3 Boundary Information for 4-Stage Design).