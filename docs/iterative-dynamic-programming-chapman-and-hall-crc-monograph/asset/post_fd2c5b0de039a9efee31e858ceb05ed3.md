
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

## Preliminary run

For a preliminary run we chose $P=10$ stages each of length 1 min initially, $R=25$ random points, $N=1$ grid point, $\gamma=0.95$, 20 iterations per pass, 20 passes with region restoration factor $\eta=0.85$, initial temperature of 723.15 for each stage, and initial region size for the temperature of 50 and for the stage lengths 0.01.

The run took 42.3 s on a PentiumII/350, and resulted in the temperature profile shown in Figure 9.8. There are 4 distinct stages. Of the original 10 stages, the first four collapsed to the lower limit with a total length of 3.595 min; the next stage of length 1.369 min yielded the upper limit; the sixth stage of length 0.901 min gave a temperature of 699.50; and the last four stages collapsed to a single stage on the lower boundary. The value of the performance index is \(I = 0.35377\) and \(t_f = 9.368\) min. It is interesting to note that this four-stage control policy gives a marginally better value than the maximum yield of 0.35375 obtained by control vector iteration procedure by Luus [7].

## Next run

For the next run, we chose the same parameters for IDP as before. For initial conditions, we divided the third stage into seven stages, each of length 1.369/7 min and kept the other three stages as obtained in the preliminary run. For these seven stages we took an initial temperature of 723.15. For the other three stages we used the values obtained in the preliminary run. After 20 passes we obtained a 9-stage control policy shown in Figure 9.9 with \(I = 0.353820\) and \(t_f = 9.283\) min. This value of the performance index is marginally better than 0.353794 obtained by Rosen and Luus [16], and just very slightly less than 0.353821 obtained by Bojkov and Luus [2] with the use of \(P = 20\) flexible stages. Although Bojkov and Luus used more than 1 grid point, we found here that a single grid point worked very well.

![](img/06ae75163df4fdf5e1eec243d497d393_174_0.png)

Figure 9.8: Four-stage optimal control policy for the pyrolysis problem resulting from the preliminary run, yielding \(I = 0.3537724\)

![](img/06ae75163df4fdf5e1eec243d497d393_175_0.png)

Figure 9.9: 9-stage optimal control policy for the pyrolysis problem, yielding $I = 0.3538200$

### 9.3.2 Modified Denbigh reaction scheme

Let us now consider the system of reactions used by Denbigh [3] and by Aris [1] with a small modification by adding the reaction where the desired product is converted into waste, as was done by Luus and Dong [12]. The reaction scheme is

$$\begin{aligned}
A + B &\longrightarrow X\\
A + B &\longrightarrow P\\
X &\longrightarrow Y\\
X &\longrightarrow Q\\
Y &\longrightarrow Z
\end{aligned}$$

where $X$ is an intermediate, $Y$ is the desired product, and $P$, $Q$, and $Z$ are waste products. It is desired to maximize the yield of $Y$ by choosing the temperature of the reactor as a function of time. Although there are seven chemical species, we are concerned only with the concentrations of $A$, $X$, and $Y$, and therefore choose as state variables their concentrations expressed as mole fractions, respectively. The equations describing the system are

$$\frac{dx_1}{dt} = -k_1x_1-k_2x_1 \tag{9.29}$$

$$\frac{dx_2}{dt} = k_1x_1-(k_3+k_4)x_2 \tag{9.30}$$

![](img/06ae75163df4fdf5e1eec243d497d393_177_0.png)

Figure 9.11: 14-stage optimal control policy for the modified Denbigh reaction scheme giving a bitumen yield of 0.54927

Luus and Dong [12] considered the case where the final time $t_f$ was specified as 500 s. Here, we consider the case where $t_f$ is not specified, but we do not want it to be excessively large. Therefore we introduce a penalty for the final time, and choose the performance index in the form

$$I=x_3(t_f)-\theta t_f \tag{9.35}$$

where the choice of the penalty function factor $\theta$ influences the final time obtained at the optimum. It will be interesting to see if we can find the value for $\theta$ which will give a final time of approximately $t_f=500$ s.

## Preliminary run

We took $P=10$ time stages each of length 40 s, $N=1$ grid point, $R=25$ randomly chosen values for control and stage length, $\gamma=0.95$, $\eta=0.85$, penalty function factor $\theta=10^{-6}$, 20 iterations per pass and allowed 20 passes. The initial temperature was chosen as 344 for each stage, the initial region size for the temperature was 142 and the initial region size for the stage length was 1.0.

Convergence to $x_3(t_f)=0.54530$ resulted with the 5-stage control policy shown in Figure 9.10. The final time $t_f=508.35$ s.

## Next run

For a more refined control policy, the stages where the control was on the lower and upper bound were left as calculated, but the remaining 3 stages were each split into

![](img/06ae75163df4fdf5e1eec243d497d393_178_0.png)

Figure 9.12: Effect of the region restoration factor η on convergence rate, showing the deviations of the yield from the optimum 0.54928 as a function of the pass number

4 stages, resulting in a 14-stage initial control policy. The initial region sizes were reduced by a factor of 10 from the values used in the preliminary run (i.e., 14.2 for the temperature and 0.1 for the stage lengths), the number of passes was doubled to 40, the number of iterations in each pass was increased to 30, and the region restoration factor η was increased to 0.95.

Convergence to x3(tf) = 0.54927 resulted in a computation time of 3843 s on a PentiumII/350 for 40 passes, giving the 14-stage control policy in Figure 9.11. This value of the yield is very close to 0.54937 obtained by Luus and Dong [12] by using 37 time stages and final time tf = 500 s. By using 50 stages, Bojkov and Luus [2] obtained a yield of 0.54948 with a final time of 508.4 s. The region restoration factor here had to be chosen sufficiently large to avoid premature collapse of the search regions as is shown in Figure 9.12. From this figure it is quite obvious that the initial region sizes have been chosen too small, preventing us from using a smaller value for the restoration factor η. It should also be possible to reduce the number of randomly chosen candidates for control and stage lengths.

To see whether R could be reduced by a better initial choice for region sizes, and also to gain better accuracy by using a larger number of stages, we followed the strategy as suggested by Luus [9]. Let us take a total of P = 30 stages. Initially the first stage was taken of length 89 s and stage 27 was taken of length 332 s, with control values of 273 and 415 respectively. The remaining 28 stages were initially chosen of length 0.5 s with control value of 344. The initial region size for each stage length was taken as 5 and the initial region size for control was taken as 25. The
