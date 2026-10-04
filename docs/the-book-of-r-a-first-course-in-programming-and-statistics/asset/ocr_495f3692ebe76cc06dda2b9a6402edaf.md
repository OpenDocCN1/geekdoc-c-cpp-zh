Continuing the example, the dermatologists want to determine whether their records suggest there is statistical evidence to indicate some relationship between the type of treatment and the level of success in curing the skin affliction. For convenience, store the total number of categories $k_r$ and $k_c$ for the row and column variables, respectively.

```
R kr <- nrow(skin)
R kc <- ncol(skin)
```

You have $O_{\{i,j\}}$ in skin, so you now must compute the $E_{\{i,j\}}$ in light of Equation (18.13), which deals with row and column sums, you can evaluate these using the built-in rowSums and colSums functions.

```
R rowSums(skin) Tablet
Injection Laser Herbal
    45 168 46 96
R colSums(skin)
None Partial Full
    112 121 122
```

These results indicate the totals in each group, regardless of the other variable. To get the expected counts for all cells of the matrix, Equation (18.13) requires each row to be multiplied by each column sum once. You could write a for loop, but this would be inefficient and rather inelegant. It is better to use `rep` with the optional argument (refer to Section 2.3.2). By repeating each element of the column totals to multiply that repeated vector by the shorter vector produced by rowSums, You can then call sum(skin) to divide this by $N$ and arrange it into a matrix. The following lines show how this works-by-step:

```
R rep(colSums(skin),each=kr)
None None None Partial Partial Partial Full
    112 112 112 121 121 121 121 122
Full Full Full
    122 122 122
```

```
R rep(colSums(skin),each=kr)*rowSums(skin)
None None None Partial Partial Partial Full
    5040 18816 5152 10752 5445 20328 5566 11616 5490
Full Full Full
    20496 5612 17172
```

```
R rep(colSums(skin),each=kr)*rowSums(skin)/sum(skin)
None None None Partial Partial Partial Full
    14.9179 53.0282 15.4268 30.28732 15.33803 57.26197 16.57887 32.7211
Full Full Full
    45.6479 73.75321 15.80845 32.91955
```

```
R skin.expected <- matrix(rep(colSums(skin),each=kr)*rowSums(skin)/sum(skin),
nrow=kr,ncol=kc,dimnames=dimnames(skin))
```