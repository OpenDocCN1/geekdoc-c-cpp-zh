# Table 6.2 Creating a Half-Fraction by Choosing the Runs in a Full Fraction with Constant Values for an Interaction

| run | XA | XB | XC | XD | XAXBXCXD | run | XA | XB | XC | XD |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | - | - | - | - | + | 10 | - | - | - | - | + |
| 2 | + | - | - | - | - | 11 | + | - | - | - | + |
| 3 | - | + | - | - | - | 4 | + | + | - | - | + |
| 4 | + | + | - | - | + | 13 | - | - | - | + | + |
| 5 | - | - | + | - | - | 6 | + | - | - | + | - |
| 6 | + | - | + | - | + | 7 | - | + | + | + | - |
| 7 | - | + | + | - | - | + | 16 | + | + | + | + | + |
| 8 | + | + | + | + | - | + | | | | | |
| 9 | - | - | - | + | - | | | | | | |
| 10 | + | - | - | + | + | | | | | | |
| 11 | - | + | - | + | + | | | | | | |
| 12 | + | + | - | + | - | | | | | | |
| 13 | - | + | + | + | + | | | | | | |
| 14 | + | - | + | + | - | | | | | | |
| 15 | - | + | + | + | + | | | | | | |
| 16 | + | + | + | + | + | | | | | | |

In preliminary experiments involving a large number of factors, usually only a small proportion of the factors will have significant effects. This fact has been called the *effect sparsity principle* by Box and Meyer (1986a). Just as two planets will line up with the moon in the night sky more often than three planets will, main effects are more likely to be important than two-factor interaction, and two-factor interactions are more likely to be important than three-factor interactions, etc. This general rule has been called the *hierarchical ordering principle* by Wu and Hamada (2000). Therefore, if fractions of factorial experiments can be planned in a way that main effects are confounded with three-factor and higher-order interactions, the amount of information lost by fractating the number of runs will be small in comparison to the benefit of a reduced number of runs.

The way a fractional factorial of a 2<sup>k</sup> is created in practice is actually the opposite of what was shown above. Instead of starting with a full factorial and eliminating runs to get the desired fraction, start with a full factorial containing the desired number of runs and add additional factors to the design.