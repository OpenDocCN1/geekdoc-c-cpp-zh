The PLAN Procedure

Plot Factors

| Factor | Select | Levels | Order |
|---|---|---|---|
| block | 4 | 4 | Ordered |
| flower | 4 | 4 | Ordered |

Treatment Factors

| Factor | Select | Levels | Order |
|---|---|---|---|
| treatment | 4 | 4 | Random |

block ---flower--- ---treatment---
1 1 2 3 4 2 4 1 3
2 1 2 3 4 1 3 4 2
3 1 2 3 4 2 3 4 1
4 1 2 3 4 3 1 4 2

# 4.3 Model for RCB

The model for the analysis of an RCB design is

\( y_{ij} = \mu + b_i + \tau_j + \epsilon_{ij}, \) (4.1)

where, \( b_i \) represent the block effects, \( \tau_j \) represent the treatment effects. The usual assumptions of normality of experimental error and homogeneity of variance for experimental error across levels of the treatment factors and blocks are required for this model. These assumptions can be checked with residual plots as shown in Section 2.4.

Notice that this is an additive model which does not include the interaction between block and treatment. Since there are only \( t \times b \) experimental units, there would be zero degrees of freedom for the error term \( ssE \) if a block by treatment interaction term were included in the model. However, the block by treatment interaction is in fact the correct error term for testing the treatment effects. The experimenter wants to generalize his conclusions about treatment effects over all the experimental units, so the average treatment effects should be larger than any differences in treatment effects among blocks of experimental units. The difference in treatment effects among blocks is exactly what the interaction measures and is therefore the correct error term. By leaving the interaction out of the model, the \( ssE \) becomes identical to the interaction sums of squares.

The ANOVA table for an RCB design is shown symbolically in Table 4.1. Representations for the type I sums of squares for blocks and treatments are shown in the table, similar to what was shown in Section 3.5.1, but they