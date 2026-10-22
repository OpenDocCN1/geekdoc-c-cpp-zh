We might also hypothesize that the effect of articles is greater for men than for women. We can test this by including an interaction between ARTS and FEMALE by modifying the MODEL statement as follows:

```
MODEL promo = female dur dur*dur select arts prestige arts*female;
```

This produced the results in Output 3.32, which clearly show some evidence for an interaction. For males, each additional article increases the odds of promotion by 100[exp(.072172)-1] = 7.5 percent. For females, each additional article increases the odds of promotion by 100[exp(.072172-.037546)-1] = 3.5 percent. This difference suggests that men get a greater payoff from their published work than do females, a conclusion that many would find troubling.

# Output 3.32 PROC QLIM Output with Interaction between FEMALE and ARTS

| Parameter Estimates |
| Parameter | DF | Estimate | Standard Error | t Value | Approx Pr > |t| |
| Intercept | 1 | -7.000433 | 0.537359 | -13.03 | <.0001 |
| FEMALE | 1 | 0.009973 | 0.201160 | 0.05 | 0.9605 |
| dur | 1 | 1.720148 | 0.164252 | 10.47 | <.0001 |
| dur*dur | 1 | -0.125284 | 0.014154 | -8.85 | <.0001 |
| select | 1 | 0.152113 | 0.046039 | 3.30 | 0.0010 |
| arts | 1 | 0.072172 | 0.011319 | 6.38 | <.0001 |
| prestige | 1 | -0.393508 | 0.088585 | -4.44 | <.0001 |
| FEMALE*arts | 1 | -0.037546 | 0.015789 | -2.38 | 0.0174 |

The danger with this conclusion is that it assumes that the degree of residual variation is the same for men and for women. In the case of assistant professors, there is reason to believe that women have more heterogeneous career patterns than men, especially during the period covered by the data used here. Hence, unmeasured variables affecting the chances of promotion may be more important for women than for men, leading to a larger value of σ for women than men in equation (3.20). That difference could explain why the effect of articles appears to be greater for men than for women.