```
/* Exit program. */
return 0;
}
/**
* This function generates a random
* double value between a and b (a<b).
*/
double rand_float(double a,double b)
{
    return ((double)rand()/RAND_MAX)*(b-a) + a;
}
```

# ## 5. TESTING

If we use the data from the hand example, we have the following interaction, wherein output matches the data that we computed by hand:

```
Enter individual component reliability:
0.8
Enter number of trials:
3
Enter unsigned integer seed:
47
Analytical Reliability
Series: 0.512 Parallel: 0.992
Simulation Reliability, 3 trials
Series: 0.667 Parallel: 1.000
```

Here are results from two more simulations which demonstrate that the simulation results approach the analytical results as the number of trials increases:

```
Enter individual component reliability:
0.8
Enter number of trials:
100
Enter unsigned integer seed:
123
Analytical Reliability
Series: 0.512 Parallel: 0.992
Simulation Reliability, 100 trials
Series: 0.470 Parallel: 1.000
```

```
Enter individual component reliability:
0.8
Enter number of trials:
1000
Enter unsigned integer seed:
3535
Analytical Reliability
Series: 0.512 Parallel: 0.992
Simulation Reliability, 1000 trials
Series: 0.530 Parallel: 0.990
```