# 3. HAND EXAMPLE

For the hand example, we use a component reliability of 0.8 and three trials. Since each trial requires three random numbers, assume that the first nine random numbers generated are the following. (These were generated from the `rand_float` function using a seed of 6,666 for values between 0 and 1.)

The first set of three random values is

```
0.939775 0.0422243 0.929037
```

The second set of three random values is

```
0.817733 0.211689 0.9909
```

The third set of three random values is

```
0.0377037 0.103508 0.407272
```

From each group of three random numbers, we can determine whether a series configuration would work properly and whether a parallel configuration would work properly. For the first and second groups of three random numbers, two of the values are greater than 0.8, so only the parallel configuration would work properly. Both configurations work properly with the third set of random numbers. Thus, the analytical results (computed earlier in this section) and the simulation results for three trials are the following:

```
Analytical Reliability:
Series: 0.512 Parallel: 0.992
Simulation for 3 Trials
Series: 0.333333 Parallel: 1
```

As we increase the number of trials, the simulation results should approach the analytical results. If we change the random-number seed, the simulation results may also change, even with only three trials.

# 4. ALGORITHM DEVELOPMENT

We first develop the decomposition outline because it divides the solution into a series of sequential steps.

# Decomposition Outline

+   1. Read component reliability, number of trials, and random-number seed.
+   2. Compute analytical reliabilities.
+   3. Compute simulation reliabilities.
+   4. Print comparison of reliabilities.

Step 1 involves prompting the user to enter the necessary information and then reading it. Step 2 uses the equations given earlier to compute the analytical reliabilities. Because the computations are straightforward, we compute them in the `main` function.