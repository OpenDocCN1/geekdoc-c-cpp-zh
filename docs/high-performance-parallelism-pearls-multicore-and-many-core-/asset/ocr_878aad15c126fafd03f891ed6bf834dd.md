# American option approximation  
parallelization gain  
(unit: K options/second, 1/56 threads, 125.9 million options)

![](bbox=[0.155, 0.081, 0.822, 0.281])

FIGURE 8.26  
American option approximation gain on parallelization on an Intel Xeon processor.

```
```cpp
#include <sys/time.h>
#include <time.h>

#pragma omp parallel
{
#ifdef _OPENMP
        threadID = omp_get_thread_num();
#else
        threadID = 0;
#endif
    // allocate memory

    // Read-in the input data
#pragma omp master
        sTime = second();

#pragma vector nontemporal (CallResult)
    for (int opt = 0; opt < OptPerThread; opt++)
    {
        float T = OptionYears[opt];
        float S = StockPrice[opt];
        float X = OptionStrike[opt];
        float b = CostofCarry[opt];
        float v = Volatility[opt];
        CallResult[opt] = baw_scalaroopt(S,X,RISKFREE,b,v,T);
    }

#pragma omp master
    {
        eTime = second();
        printf(
        "Completed pricing %7.5f million options in %7.5f seconds:\n",
            OPT_N/1e6, eTime-sTime);
        printf(
        "Parallel version runs at %7.5f Thousand options per second.\n",
            OPT_N/(1e3*(eTime-sTime)));
    }
    // de-allocate memory
}
```
```

FIGURE 8.27  
Core parallelization using OpenMP4.0 for American options approximation.