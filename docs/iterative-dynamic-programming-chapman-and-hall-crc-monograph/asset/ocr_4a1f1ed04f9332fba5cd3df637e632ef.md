```
$$x_7=\frac{2}{x_3+x_4+2x_5}$$ (1.108)

$$x_6=x_7\left(0.5(x_1+x_3)+x_2\right)$$ (1.109)

$$f_1=x_1+x_2+x_5-\frac{1}{x_7}=0$$ (1.110)

$$f_2=-28837x_1-139009x_2-78213x_3+18927x_4+8427x_5+\frac{13492-10690x_6}{x_7}=0$$ (1.111)

$$f_3=x_1+x_2+x_3+x_4+x_5-1=0$$ (1.112)
```

The equations may also be arranged into the structure where we have five simple equalities and only two difficult equality constraints:

```
$$x_3=\frac{5.2116x_2(x_1+x_2)}{x_1+2.6058x_2}$$ (1.113)

$$x_4=2(x_1+x_2)-x_3$$ (1.114)

$$x_5=\frac{400x_1x_4^3}{1.7837\times10^5x_3}$$ (1.115)

$$x_7=\frac{2}{x_3+x_4+2x_5}$$ (1.116)

$$x_6=x_7\left(0.5(x_1+x_3)+x_2\right)$$ (1.117)

$$f_1=-28837x_1-139009x_2-78213x_3+18927x_4+8427x_5+\frac{13492-10690x_6}{x_7}=0$$ (1.118)

$$f_2=x_1+x_2+x_3+x_4+x_5-1=0$$ (1.119)
```

Since the first 5 variables denote mole fractions, it should be possible to make reasonable choices for the first 3 variables in the first arrangement and for the first 2 variables in the second arrangement. Although, as reported by Shacham [28] this problem was too difficult for most of the programs he evaluated, there were no difficulties with the recommended procedure. For stability in calculations, if any of the $x_i$, $i=1,\ldots,n$ would be less than $10^{-4}$, the corresponding variable was put to $10^{-4}$, and similarly the upper clipping limit of 0.95 was used. Convergence profiles from the starting point $x_1=0.22$, $x_2=0.075$, $x_3=0.001$ for the first formulation of this problem with three difficult equality constraints and from $x_1=0.22$, $x_2=0.075$ for the second formulation are shown in [Figure 1.5](#).