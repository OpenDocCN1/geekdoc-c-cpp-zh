# TABLE 17.16 Rotated Factor Pattern Matrix for the Olympic Athlete Data Using VARIMAX Rotation

| | Factor1 | Factor2 | Factor3 |
|---|---|---|---||
| run100 | 100 meters | 0.84580 | 0.23258 | -0.07671 |
| longjump | long jump | 0.60647 | 0.36590 | 0.33100 |
| shotput | shot put | 0.30160 | 0.77719 | -0.20041 |
| highjump | high jump | 0.17997 | 0.49795 | 0.31233 |
| run400 | 400 meter run | 0.70075 | 0.04678 | 0.34054 |
| hurdles | 110 meter hurdles | 0.68461 | 0.36227 | 0.04849 |
| discus | discus | 0.21230 | 0.72866 | -0.20384 |
| polevault | pole vault | 0.31426 | 0.42324 | 0.26363 |
| javelin | javelin | 0.07697 | 0.52602 | 0.22676 |
| run1500s | 1500 meter run | 0.09184 | -0.01599 | 0.60519 |

# 17.2 SUMMARY

In this chapter, we have discussed methods for using PROC FACTOR to perform exploratory factor analysis. In the Hands-on Example, we have illustrated the use of rotation to obtain more understandable results.

# EXERCISES

17.1 Run a factor analysis on the intelligence data using principal components.

+   a. Modify the file AFACTOR1.SAS to run a principal component analysis by removing the PRIORS-SMC option.
b. What are the initial communalities?
c. Compare and contrast the results with those obtained using principal factors method used in the first Hands-on Example. Do you arrive at similar factors?
d. Find the correlation between new variables Factor1 and Factor2? Do the rotated factors appear to be uncorrelated (orthogonal)?

17.2 Run a factor analysis on the Olympic Athlete Data using maximum likelihood.

+   a. Modify the file AFACTOR2.SAS to perform factor analysis on the Athlete Data using maximum likelihood.
b. Compare and contrast the results with those obtained using principal factors method used in the first Hands-on Example. Are the interpretations the same?