Table 9.2: Kinetic parameters for the pyrolysis problem

| Reaction $i$ | $a_i$ | $b_i$ |
|---:|---:|---:|
| 1 | 8.86 | 20300/1.9872 |
| 2 | 24.25 | 37400/1.9872 |
| 3 | 23.67 | 33800/1.9872 |
| 4 | 18.75 | 28200/1.9872 |
| 5 | 20.70 | 31000/1.9872 |

with the initial condition

$$x(0)=[\,1\ 0\ 0\ 0\,]^T.$$  \tag{9.25}

The rate constants are given by

$$k_i=\exp\left(a_i-\frac{b_i}{T}\right),\qquad i=1,2,\ldots,5, \tag{9.26}$$

where the kinetic parameters $a_i$ and $b_i$ are given in **Table 9.2**. The optimal control problem is to find both the residence time $t_f$ and the temperature $T$ in the time interval $0<t<t_f$, so that the concentration of pyrolytic bitumen given by $x_2$ is maximized. The performance index to be maximized is thus

$$I=x_2(t_f). \tag{9.27}$$

The constraints on the temperature are

$$698.15\leq T\leq 748.15. \tag{9.28}$$

By using control vector iteration based on Pontryagin’s maximum principle, Luus [7] solved this optimal control problem by fixing $t_f$ at 17 different values and then interpreting the results to conclude that the maximum value of the performance index of 0.35375 occurs at $t_f=9.5$ min. Rosen and Luus [16] improved the value to $I=0.35379$ at time $t_f=9.123$ min. By using IDP with $P=80$ time steps of equal length, Luus [9] obtained $I=0.35382$ at $t_f=9.3$ min. By using flexible stage lengths in IDP, Bojkov and Luus [2] obtained $I=0.35381$ with $P=5$ time stages and $I=0.35382$ with $P=10$ flexible stages. Let us examine this latter approach.

# Preliminary run

For a preliminary run we chose $P=10$ stages each of length 1 min initially, $R=25$ random points, $N=1$ grid point, $\gamma=0.95$, 20 iterations per pass, 20 passes with region restoration factor $\eta=0.85$, initial temperature of 723.15 for each stage, and initial region size for the temperature of 50 and for the stage lengths 0.01.