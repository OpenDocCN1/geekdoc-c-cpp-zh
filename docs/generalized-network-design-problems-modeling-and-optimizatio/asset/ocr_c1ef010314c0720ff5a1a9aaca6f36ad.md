# Experimental setup

We have implemented our algorithm as part of a software package written in Java, which is available online at http://swarmst.sourceforge.net/. At this address we provide all information necessary to reproduce our experiments.

In all experiments, we used candidate lists of length 4. The other parameters of the algorithm have been tuned, using the paramILS configuration framework [83]. We have generated a set of 100 Euclidean TSP instances with n cities, uniformly distributed in the interval [200, 500] and with coordinates uniformly distributed in a space of dimension 10000 x 10 000.

These instances have then been converted to the GTSP by applying the CLUSTERING procedure introduced in [43]. This procedure sets the number of clusters s = ceil(n/5), identifies the s nodes farthest from each other and assigns each remaining node to its nearest center. We have used the resulting GTSP instances as training data for paramILS.

Before starting the tuning procedure, we ran our algorithm 10 times on each instance in the training set, using a default configuration. Each run has been terminated after n/10 seconds and we have stored the best result obtained for each GTSP instance. During the tuning procedure, these best known results are used as termination condition for our algorithm.

Each time paramILS evaluates a parameter configuration with respect to a given instance, we determine the mean time (averaged over 10 trials) that our algorithm

![](bbox=[0.1, 0.53, 0.9, 0.86])

Figure 3.5. The generalized 2-opt exchange.