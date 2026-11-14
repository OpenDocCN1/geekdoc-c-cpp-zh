| Source | DF | Type III SS | Mean Square | F Value | Pr > F |
| :--- | :--- | :--- | :--- | :--- | :--- |
| subject | 11 | 24.25471000 | 2.20497364 | 86.01 | <.0001 |
| period | 1 | 0.00183750 | 0.00183750 | 0.07 | 0.7920 |
| treat | 2 | 0.63916333 | 0.31958167 | 12.47 | 0.0004 |
| carry | 2 | 0.23320556 | 0.11660278 | 4.55 | 0.0252 |

| Level of treat | N | Mean | Std Dev |
| :--- | :--- | :--- | :--- |
| cement | 12 | 6.21166667 | 0.76463697 |
| grass | 12 | 6.39916667 | 1.12488329 |
| track | 12 | 6.14083333 | 0.83989673 |

The carryover effects are summarized in the following table of means. Subtracting the grand mean from these estimates, it can be seen that the carryover effects of grass and cement are negative which means that the sprinting times will be slightly faster in the sprint following one on grass or cement. The "0" level of carryover means no prior treatment. This is where the longest sprint times occur.

| Level of carry | N | Mean | Std Dev |
| :--- | :--- | :--- | :--- |
| 0 | 12 | 6.67250000 | 0.94744753 |
| cement | 8 | 5.97375000 | 0.92968409 |
| grass | 8 | 5.94250000 | 0.80331012 |
| track | 8 | 6.20250000 | 0.80786756 |

# 9.4.2 Designs with p > t or t > p

One problem with Williams' designs is that the direct treatment effects and the carryover effects are not orthogonal. The type III ANOVA table makes a test for significance of treatment effects adjusted for treatments and a test for carryover adjusted for treatments; however, SAS proc glm is unable to produce least squares (adjusted) means for treatments and carryover due to the imbalance in these factors. In addition the direct treatment effects are estimated more precisely than the carryover effects since each marginal mean is the average of 12 observations for the direct effects but only 8 for the carryover effects.

Lucas (1957) proposed a solution to this problem by simply adding an extra period where all sequence groups receive the same treatment that they received in the 7th period. This makes the design completely balanced in the sense that every treatment follows every other treatment an equal number of times,