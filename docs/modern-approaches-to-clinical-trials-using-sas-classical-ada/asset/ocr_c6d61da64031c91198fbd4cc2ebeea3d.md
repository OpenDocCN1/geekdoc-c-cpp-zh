# 4.2.2 Input Data for a Meta-Trial Design Variable

A General Design of Meta-Trials with Two Arms shows a general survival meta-experimental design setting for $K$ randomized trials with two arms introduced in the previous section. From Table 4.1, we see that the input data contain trial ID (TID), the total sample size ($n$), proportion in control arm ($ho$), annualized event rate ($r$) in the control arm, trial duration (TD), and accrual time (TA) for each trial. Using the relationship between trial duration and accrual time, we calculate the minimum follow-up time (TF) for each trial; that is, $TF_k = TD_k - TA_k$. We note that these input data are used to generate the predictive data discussed in 4.6 Computational Algorithms. From the prior predictive data algorithm presented in 4.6 Computational Algorithms, we impose the constraints on $TD_k \ge 0$, $TF_k \ge 0$, $TD_k \ge TF_k$ and $TD_k > TA_k$. (4.1)

In (4.1), if all subjects enroll the trial at the trial entry time; if $TF_k=0$, there is no minimum follow-up requirement; and if $TD_k \le TF_k + TA_k$ subjects are followed-up during the entire trial after the subjects enroll in the trial. In addition, the number of studies ($K$), the number of MCMC samples (NMCS), the number of burn-in-samples ($nbi$), the number of simulated data sets ($REP$), design margin ($\varrho$), and user-defined Bayesian credible level ($n_0$) are required as input variables to run the SAS macro, BSMED, discussed in Section 4.7.

# Table 4.1 A General Design of Meta-Trials with Two Arms

| Trial ID (TID) | Sample Size ($n$) | Proportion in Control Arm ($ho$) | Annualized Event Rate ($r$) | Trial Duration (TD) | Accrual Time (TA) |
|---|---|---|---|---|--|
| 1 | $n_1$ | $ho_1$ | $r_1$ | $TD_1^A$ | $TA_1^A$ |
| 2 | $n_2$ | $ho_2$ | $r_2$ | $TD_2^A$ | $TA_2^A$ |
| ... | ... | ... | ... | ... | ... |
| $K$ | $n_k$ | $ho_k$ | $r_k$ | $TD_k^A$ | $TA_k^A$ |