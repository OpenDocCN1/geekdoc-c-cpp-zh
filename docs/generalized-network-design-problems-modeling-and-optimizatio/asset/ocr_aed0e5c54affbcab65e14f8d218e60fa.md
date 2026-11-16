on the current solution, it is accepted. Otherwise, it is accepted with a probability \(p(T, \delta) = \exp(-\delta/T)\), which depends on the control parameter \(T\) (the temperature in the physical equivalent) and the amount \(\delta\) by which the move worsens the current solution. This relation ensures that the probability of accepting a move to a very poor solution is very small. After completion of each stage, the temperature is reduced. The way the temperature is reduced is known as the *cooling schedule*. Given a relatively high temperature \(T\) at the beginning of the process, the probability of accepting a non-improving moves is fairly high. As the process continues, the temperature decreases and non-improving moves become less likely.

The search is continued until there is some evidence that suggests that the probability of improving on the best solution found so far is very low. At this stage, the system is said to be frozen.

Given a neighborhood structure, simulated annealing can be viewed as an algorithm that continuously attempts to transform the current configuration into one of its neighbors.

Comparing iterative improvement and simulated annealing, it is apparent that the situation where the control parameter in the simulated annealing algorithm is set to 0 corresponds to a version of iterative improvement. Conversely, simulated annealing is a generalization of iterative improvement in that it accepts, deterioration of the cost function, with non-zero but gradually decreasing probability. It is not clear, however, whether it performs better than repeated application of iterative improvements (for a number of different initial configurations): both algorithms converge asymptotically to a globally minimal configuration of the problem at hand.

In order to implement the simulated annealing algorithm for the GMSTP, a number of decisions must be made. These can be divided into two categories: *generic decisions*, which are concerned with parameters of the annealing algorithm itself, including factors such as the initial temperature, the cooling schedule (governed by the parameter \(L\), i.e. number of repetitions and the choice of the temperature reduction function \(\alpha\)), and the *stopping condition*, and *problem specific decisions*, involving the choice of the solution space, the form of the cost function (initialization) and the employed neighborhood structure.

In our implementation of the simulated annealing algorithm for the GMSTP, we choose the following cooling schedule:

+   1. **Initial value of the control parameter, \(T_0\).** Following Johnson et al. [90], we determine \(T_0\) by calculating the average increase in cost \(\delta^+\), for a number of random transitions:

\(T_0 = \frac{\delta^+}{\ln(\chi_0^{-1})}\)

where \(\chi_0 = 0.8\) is a given acceptance rate.