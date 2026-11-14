```
data cdesign;
do A = 0 to 1;
do B = 0 to 1;
output;
end;
end;
*creates a design with 6 blocks of size 2 i.e., structure=(b)k;
proc optex data=cdesign coding=orthcan seed=73462;
class A B;
model A|B;
blocks structure=(6)2;
generate n=12;
output out=design blockname=block;
output;
proc print data=design;
run;
```

structuring balanced confounded designs where (1) the information recovered for each degree of freedom for any partially confounded interaction is the same, and (2) any contrast of a partially confounded interaction is estimable independently of any contrast of another partially confounded interaction. The information recovered for the ith degree of freedom in the model (7.5) is calculated as c_ii / c_ii. c_ii is the diagonal of X'X^-1 matrix corresponding to particular single degree of freedom, and σ^2 c_ii is the variance of τ̂_i in a design where the treatment effects are orthogonal to blocks. c_ii is the diagonal X'QX^-1, and σ^2 c_ii is the variance of τ̂_i in the partially confounded design where Q is defined in Equation (7.7). In partially confounded designs c_ii > c_ii, but t^2σ^2 should be much smaller than σ^2 due to the fact that the experimental units are more homogenous within the blocks of reduced size.

Constructing a design using Das's method consists of converting the asymmetrical factorial into a fraction of a symmetrical factorial. The partial confounding is performed in replicates of the symmetrical factorial, and then each replicate is reduced by fractionation. Lawson et al. (2009) show how Das's method can be implemented with proc plan and the SAS data step. They also provide a SAS macro for generating Das's balanced confounded designs. Creating designs by this method will allow all interactions in the model to be estimated and will result in a design with equal precision for each single degree of freedom of partially confounded effects and interactions. One disadvantage for using this method is that the total number of treatment combinations, N = s_1^n1 × s_2^n2 × ⋯ × s_n^nn must always be divisible by the block size. This can require a large number of blocks in some cases.

Cook and Nachtheim's algorithm can also be used to find a partially confounded mixed-level factorial that will allow estimation of all interactions, and there is no restriction on the block size. Using this method can sometimes produce a balanced confounded design like Das's method, and in other cases it will find an approximately balanced design with more choices for the block size and total number of runs. Lawson et al. (2009) illustrate how partially confounded designs can be created with Cook and Nachtheim's algorithm using