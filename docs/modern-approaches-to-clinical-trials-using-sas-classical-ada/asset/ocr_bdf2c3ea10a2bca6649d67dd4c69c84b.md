```
run;

proc noobs label;
  var f alpha_a beta_a es_sub_power;
  run;
%mend subpower;
%subpower(0.5, 0.04, 0.2, 2, 0.01)
```

For example, assuming 50% prevalence of a biomarker group, an alpha split of 0.04 versus 0.01 for the overall population and the subgroup, 80% power for the overall population, effect size ratio of 2, the power to detect treatment effect in the biomarker based population is 91%.

With multiple looks and subgroups there are several multiplicity methods [38, 42, 50] that can be employed to control the family-wise error rate at a nominal level, i.e., the probability of rejecting at least one true null hypothesis. A closed testing procedure is used to control multiplicity where all the possible intersection hypotheses ($H_0^{Cp}, H_0^{Sp}, H_0^{CpSp}$) is considered for rejecting any initial hypothesis ($H_0$). The stage-wise p-values for testing $H_0^{Cp}$ and $H_0^{Sp}$ are denoted by $Cp_p$ and $Sp_p$ for each stage $i\in\{1,2\}$, while $CpSp_{p_i}$ is a function of $Cp_{p_i}$ and $Sp_{p_i}$ for accounting multiplicity multiplicity can be calculated using the Hochberg correction [51] or the Dunnett methods [52]. The final analysis is done on the overall population ($C_P$) using the inverse normal p-value combination test [53-54]. For each stage weights $w_1$ and $w_2$, where $w_1^2+w_2^2=1$, are specified to combine the p-values. The null hypothesis at the final analysis is rejected if $C(p_1, p_2)=w_1^{-1}(1-p_1)+w_2^{-1}(1-p_2) \geq c$.