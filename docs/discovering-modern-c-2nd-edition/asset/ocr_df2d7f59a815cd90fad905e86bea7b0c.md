Most STL algorithms can be performed in parallel in C++17. The according functions are overloaded with new implementations starting with an execution policy followed by the function parameters as we know them. All policies reside in namespace std::execution. To perform an algorithm sequentially (as before, we can use the policy seq or omit it altogether. Thus the following two calls are equivalent:

```
sort(seq, begin(v), end(v));
sort(begin(v), end(v));
```

# The policy par:

```
sort(par, begin(v), end(v));
```

triggers a multi-threaded execution whereas the computation is sequential in each thread. To unleash the maximal potential of the hardware, we can use par_unseq:

```
sort(par_unseq, begin(v), end(v));
```

which allows for performing the operations within each thread in parallel (i.e., unsequentially) as well. This means in practice usually that numerical operations are performed with SSE/AVX acceleration.

![](bbox=[0.14, 0.57, 0.2, 0.6])

In C++20 the policy unseq was added to compute unsequentially on a single thread. For testing a parallel sort we used Visual Studio 2019 version 16.9.3 on a four-core Intel Core i7-8550U with 1.8 GHz yielding the following wall clock times when sorting 10 million int values:

Click here to view code image

```
Sorting with seq took 0.82638s.
Sorting with par took 0.216368s.
Sorting with unseq took 0.819744s.
Sorting with par_unseq took 0.219476s.
```

We can see that the multi-threaded version is about four times as fast whereas the parallelization within the thread didn't accelerate the execution since SSE/AVX aren't of much benefit in sorting int values. However, one of the book's reviewers observed the fastest result with unseq on his