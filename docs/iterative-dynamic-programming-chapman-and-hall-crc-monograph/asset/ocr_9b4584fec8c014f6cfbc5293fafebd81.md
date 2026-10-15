10⁻⁶ in 56 iterations as is shown in Figure 1.8. The mass imbalance is defined by

```
$$M = \sum_{i=1}^{m} |F z_{iF} - D K_{i1} x_{i1} - B x_{in}|, \tag{1.152}$$
```

where F is the feed flow rate to stage F, here taken as 11, with composition z_{iF}, D is the distillate flow rate from the partial condenser with liquid composition x_{i1} and B is the bottom flow rate with liquid composition x_{in}.

The only starting points required to solve the algebraic equations are very crude estimates for the top and the bottom temperatures of the distillation column. For this particular run we chose the bottom temperature of 810 and top temperature of 510. The actual temperatures for the bottom and top stages are 764.75 and 589.84 respectively. When another run was made with initial estimates for the bottom and top temperatures of 765 and 590, 57 iterations were required for convergence. The same temperature profile was obtained and the computation time was also 0.11 s. Needless to say, such an approach is very easy to use.

# 1.10 Solving ordinary differential equations

There are numerous methods of numerically integrating a set of ordinary differential equations. For some common methods, the reader could refer to the excellent book by Carnahan et al. [5]. To balance the accuracy with speed, it has been found that the fourth order Runge-Kutta method is well suited for many problems. One has direct control over the integration time step, so that the most appropriate step size can be used for well behaved problems.

There are situations, however, when a constant step size is not appropriate, so one method which has been found very useful is an IMSL routine based on the Runge-Kutta method called DVERK, programmed by Hull et al. [9]. Here the user specifies the local error tolerance and the routine chooses the step-size required. We have found this method most useful and, with the permission of the authors, we have included the listing of DVERK in Appendix E. This routine is also available by connecting to their website, http://www.cs.toronto.edu/NA/index.html, moving to the topic Mathematical Software and clicking on DVERK.

# 1.11 References

[1] ARIS, R. AND AMUNDSON, N.R.: “An analysis of chemical reactor stability and control”, Chem. Eng. Sci. 7 (1958), 121-147.

[2] BASHEIN, G.: “A simplex algorithm for on-line computation of time optimal control problems”, IEEE Trans. Auto. Control AC-16 (1971), 479-482.