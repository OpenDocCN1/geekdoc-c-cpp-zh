```
int N = 10000;
double vec1[N];
double vec2[N];
double sum = 0.0;
int i;
#pragma omp parallel for reduction (+:sum)
for (i = 0; i < N; ++i)
    sum += vec1[i]*vec2[i];
```

# 11. (Parallelising the Finite Difference Method)

In Chapters 20 to 23 we discussed how to approximate the solution of partial differential equations using the finite difference method. We proposed a number of schemes and we give some examples (see Section 21.8 for more details):

```
CNIBVP fdmCN(currentImp, earlyExercise,N, J);
ImplicitEulerIBVP fdmIE(currentImp, earlyExercise,N, J);
ExtrapolatedImplicitEulerIBVP fdmEIE (currentImp,earlyExercise,N, J);
ADE fdmADE(currentImp, earlyExercise,N, J);
ADE_BC_CRTP fdmADE2(currentImp, earlyExercise,N, J);
ADE_Larkin_RW_CRTP fdmADE3(currentImp, earlyExercise,N, J);
ADEExtrapolated fdmADE4(currentImp, earlyExercise, N, J);
```

In general, we can think of several use cases and viewpoints to take in order to test finite difference schemes for accuracy and performance:

+   UC1: Compare the accuracy of a new finite difference scheme with an accurate baseline scheme or exact solution.
+   UC2: Stress test a scheme for a range of input parameters to the PDE. The parameters are randomly generated using the designs that we used in Chapter 16 (in particular, Section 16.4). The focus is to determine the robustness and accuracy of a scheme for a range of input parameters.
+   UC3: Compute option prices for an input data set.

We focus on questions related to case UC3.

Answer the following questions:

+   a) Adapt the code in Section 28.4 to test the Crank–Nicolson, ADE and MOL against each other. Each scheme will be run in its own thread.
+   b) Compute the option price in each case and compare the prices regarding accuracy. Concentrate on the cases where the differences are greater than a given tolerance.
+   c) Extend the code in parts a) and b) to the case where the input data is generated using the techniques we used in Section 16.4. Create a loop with a given number of iterations and compute the global maximum error between the solutions from all runs of random generation of the input data.

The advantage of this approach is that you can run the program in batch mode as it were, and when you come back from lunch it will give output on the accuracy of the scheme that you are testing.