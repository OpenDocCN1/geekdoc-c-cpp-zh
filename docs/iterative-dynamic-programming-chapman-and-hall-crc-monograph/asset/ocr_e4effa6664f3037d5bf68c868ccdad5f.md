![](bbox=[0.357, 0.092, 0.67, 0.405])

Figure 9.11: 14-stage optimal control policy for the modified Denbigh reaction scheme giving a bitumen yield of 0.54927

Luus and Dong [12] considered the case where the final time $t_f$ was specified as 500 s. Here, we consider the case where $t_f$ is not specified, but we do not want it to be excessively large. Therefore we introduce a penalty for the final time, and choose the performance index in the form

$$I=x_3(t_f)-\theta t_f \tag{9.35}$$

where the choice of the penalty function factor $\theta$ influences the final time obtained at the optimum. It will be interesting to see if we can find the value for $\theta$ which will give a final time of approximately $t_f=500$ s.

# Preliminary run

We took $P=10$ time stages each of length 40 s, $N=1$ grid point, $R=25$ randomly chosen values for control and stage length, $\gamma=0.95$, $\eta=0.85$, penalty function factor $\theta=10^{-6}$, 20 iterations per pass and allowed 20 passes. The initial temperature was chosen as 344 for each stage, the initial region size for the temperature was 142 and the initial region size for the stage length was 1.0.

Convergence to $x_3(t_f)=0.54530$ resulted with the 5-stage control policy shown in [Figure 9.10](#). The final time $t_f=508.35$ s.

# Next run

For a more refined control policy, the stages where the control was on the lower and upper bound were left as calculated, but the remaining 3 stages were each split into