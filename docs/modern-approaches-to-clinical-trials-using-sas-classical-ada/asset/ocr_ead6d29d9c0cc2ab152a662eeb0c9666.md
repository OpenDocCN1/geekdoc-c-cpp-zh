# 10.3.1 Preliminaries

Optimal allocation rules discussed in Section 10.2 depend on treatment success probabilities $p_E$ and $p_C$. For the time being let us assume that $p_E$ and $p_C$ are known. Furthermore, suppose that all $n$ eligible patients are available for the trial at once. Then, if we want to implement, say, RSIHR allocation (2), we would have to split the $n$ patients into two groups of sizes $n_E$ and $n_C$, where

```
$n_E = n\frac{\sqrt{p_E}}{\sqrt{p_E\|+\sqrt{p_C}}$ and $n_C = n - n_E$
```

$(n_E$ and $n_C$ can be rounded up to integers if necessary).

However, there are several potential issues with this approach. First, it is infeasible to have all $n$ patients at once. Most clinical trial years to run and el eligible patients are recruited over time. Second, in practice $p_E$ and $p_C$ are unknown, and in fact the trial is to estimate $p_E$ and $p_C$. Third, study patients cannot be simply "split" into two treatment groups—an investigator may be subjective when deciding on treatment assignments and may introduce bias into the design.

RAR can be used to target the desired optimal allocation. The idea of RAR is to use accumulating data (outcomes) from patients in the trial to estimate $p_E$ and $p_C$ and modify treatment randomization probabilities for the current patient so that the design converges to the desired target allocation. By convergence of the design we mean that the sample treatment allocation proportions converge to the corresponding target allocation proportions. RAR requires that primary data are unmasked periodically or sequentially for the purpose of estimating $p_E$ and $p_C$ and updating randomization probabilities. In practice, RAR trials must be conducted by a centralized randomization unit, and the roles and responsibilities of the study personnel involved in data collection, data cleaning, data analysis, and generation of treatment assignments must be clearly defined in the trial protocol [2,45].

We now describe the basic setup for RAR. The trial starts with