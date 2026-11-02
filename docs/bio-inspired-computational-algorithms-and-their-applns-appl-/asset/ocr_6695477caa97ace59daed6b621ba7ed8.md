![](bbox=[0.13, 0.1, 0.89, 0.42])

Fig. 3. Upper and lower bounds provided by Benders’ algorithm (BD-Opt).

![](bbox=[0.13, 0.5, 0.89, 0.83])

Fig. 4. Incumbent Solution Found by Benders’ algorithm (BD-Opt).

Finally, the algorithm was again restarted, and 50 trial solutions were evaluated by the subproblems, this time using a genetic algorithm, so that the master problem is again suboptimized to generate the trial solutions. Each master problem was terminated after 40 trial solutions better than the incumbent have been found (or after a maximum of 100