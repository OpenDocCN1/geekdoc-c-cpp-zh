an individual mutates, this is mutated as many times as the value of the integer part that has in the repetition of mutation of himself. To apply the mutation to an individual a coordinate of the vector is chosen at random, and it is changed its value for another (chosen also at random) between the limits established for the above mentioned coordinate. The multiple mutation is the application of this procedure to the same individual several times.

# 3.2 Use of the self adaptive genetic algorithms

Since SAGA are random, it is common to realize several runs on the same problem and choose the best result from them. These algorithms are applied in three stages to solve our problems. In the first two stages are defined which are the important variables to solve the problem, and in the third stage, it is where the solution is calculated properly. It is important to note that the individuals have two parts, but in this section only there is born in mind the first part of the individual, which corresponds to the Autoregressive components. Here is the procedure based on SAGA, which is performed to obtain a solution to the problem.

In the first stage are used SAGA to explore the space of solutions and later to define which variables among δ, φ1, φ2, ..., φp, are the most important for the problem in question. For this were done 10 repetitions of 1000 iterations each, and with the solutions of each repetition, a vector is constructed by the sum of the absolute values of δ, φ1, φ2, ..., φp, (see Figure 1)

![](bbox=[0.25, 0.66, 0.8, 0.78])

Fig. 1. Solution using all variables.

In this first stage, the aim is to realize an exploration of the space of solutions, and for that are performed 10 iterations with all variables to consider. Then, with the 10 solutions obtained, a vector is built by adding the 10 solutions with all its positive components, and it is assumed that the largest values of these components are the most important.

In the second stage the SAGA are applied to find solutions by considering only the important variables of the problem. For this is defined in advance how many variables are required (this will be seen to detail below), and are chosen those which correspond to larger values of the first stage. In this stage 5 repetitions are realized, where each one is finished until the optimum is not modified in the last 200 iterations. Of these 5 repetitions the best result obtained is chosen (see Figure 2).

In this second stage, only are considered the variables that had greatest values in the part of the autoregressive components of the individual, and for them are kept the original intervals of its values: For all the other variables in this part of the individual, it is stated that the upper and lower limits are zero. In this stage 5 repetitions are realized and from them is chosen the one that has lower value of RSS.

In the third stage it will be found the solution in which only are taken into account the important variables obtained in the previous stage. For this are extended the boundaries