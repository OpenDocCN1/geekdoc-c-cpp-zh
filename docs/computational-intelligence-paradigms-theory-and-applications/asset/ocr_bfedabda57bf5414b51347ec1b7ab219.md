It is therefore important that these evaluations should be performed efficiently and is essential if the optimization is to be performed on a serial computer.

Like GAs, ESs are particularly well-suited to implementation on parallel computers. Evaluation of the objective function and constraints can be done simultaneously for a whole population, by mutation and recombination.

If it is possible to parallelize the evaluation of individual problem functions effectively, some thought and, perhaps, experimentation will be needed to determine the level at which multitasking should be performed. This will depend on the number of processors available, the intended population size and the potential speed-ups available. If the number of processors exceeds the population size, multi-level parallelization may be possible.

# ### Pseudocode

The pseudocode of ES is shown below:

```
```
t=0
initialize(P(t=0));
evaluate(P(t=0));
while is Not Terminated () do
P_r(t) = selectBest (μ, P(t));
P_c(t) = reproduce (λ, P_p);
mutate(P_c(t));
evaluate(P_c(t));
if (use Plus Strategy) then P(t+1) = P_c(t) ∪ P(t);
else P(t+1) = P_c(t);
t = t + 1;
end
```
```

# ### 11.9.7 Algorithm Performance

Figure 11.10 shows the progress of an ES on the two-dimensional Rosenbrock function, f = (1 − x1)^2 + 100(x2 − x1^2)^2. Each member of the 1st, 10th, 20th, and 30th generations is shown (by a symbol), although, in fact, most of the members of the 1st generation lie outside the bounds of the figure. The convergence of the population to the neighborhood of the optimum at (1,1) is readily apparent. Notice how the 20th generation appears to be converging on (0.75,0.7), but in the