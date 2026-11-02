Variations on this theme include choosing any number of variables to modify and generate different β for each variable. This method also allows generations of offspring outside the value ranges of the two parent variables. If this happens, the offspring is discarded and the algorithm tries to use another β. The blend crossover (BLX-α) method [Randy L. Haupt & Sue Ellen Haupt, 2004] begins by choosing some parameters that determine the distance outside the bounds of the two parent variables that the offspring variable may lay. This method allows new values outside of the range of the parents without letting the algorithm stray too far.

The algorithm is a combination of an extrapolation method with a crossover method. The goal was to find a way to closely mimic the advantages of the binary GA mating scheme. It begins by randomly selecting a variable in the first pair of parents to be the crossover point:

```
α = roundup{random * N_var}  (13)

Let
parent₁ = [p_m1 ... p_mα ... p_mN_var]
parent₂ = [p_d1 ... p_dα ... p_dN_var]  (14)
```

where the m and d subscripts discriminate between the mom and the dad parent. Then the selected variables are combined to form new variables that will appear in the children:

```
pnew₁ = p_mα - β[p_mα - p_dα]  (15)
pnew₂ = p_dα + β[p_mα - p_dα]
```

where β is a random value between 0 and 1. The final step is to complete the crossover with the rest of chromosome:

```
offspring₁ = [p_m1 p_m2 p_new1 ... p_mN_var]  (16)
offspring₂ = [p_d1 p_d2 p_new2 ... p_mN_var]
```

where β is also a random value between 0 and 1. The final is to complete the crossover with the rest of the chromosome as before:

If the first variable of the chromosomes is selected, then only the variables to the right of the selected variable are swapped. If the last variable of the chromosomes is selected, then only the variables to the left of the selected variable are swapped. This method does not allow offspring variables outside the bounds set by the parent unless β > 1.

# 2.4.2.1.6 Mutation

If care is not taken, the GA can converge too quickly into one region on the cost surface. If this area is in the region of the global minimum, there is no problem. However, some functions have many local minima. To avoid overly fast convergence, other areas on the cost surface must be explored by randomly introducing changes, or mutations, in some of the variables. Random numbers are used to select the row and columns of the variables that are to be mutated [Randy L. Haupt & Sue Ellen Haupt, 2004].