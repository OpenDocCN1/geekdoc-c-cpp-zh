| 1 | $y_{011}$ | $v_{011}$ | 0 | 1 | $y_{011}$ | $v_{011}$ | 0 |
| 1 | $y_{021}$ | $v_{021}$ | 1 | 1 | $y_{021}$ | $v_{021}$ | 1 |
| 2 | $y_{012}$ | $v_{012}$ | 0 | 2 | $y_{022}$ | $v_{022}$ | 1 |
| 2 | $y_{022}$ | $v_{022}$ | 1 | 3 | $y_{013}$ | $v_{013}$ | 0 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| $K_0$ | $y_{0K_0}$ | $v_{0K_0}$ | 0 | $K_0$ | $y_{01K_0}$ | $v_{01K_0}$ | 0 |
| $K_0$ | $y_{02K_0}$ | $v_{02K_0}$ | 1 | $K_0$ | $y_{02K_0}$ | $v_{02K_0}$ | 1 |

From Types of Single-Arm Historical Data and Types of Multi-Arm Historical Data, we see that for the Type IV, the historical data are available for both arms for some studies and for the experimental arm for some other studies in a mixed fashion. For instance, the historical data are available only for the control arm in TID 3 ($x_{Q3}=0$, scalar), only for the experimental arm in TID 2 ($x_{Q2}=1$, scalar), and for both arms in TID 1, the vector $x_{01}=(x_{011},x_{021})=(0,1)$ from historical studies. We note that historical data contain $y_{0K}, v_{0K}$ and $x_{0K}$. Moreover, the number of studies ($K_0$) and the discounting parameter ($a_0$) are also two input variables for the historical data in the SAS macro

BSMED.