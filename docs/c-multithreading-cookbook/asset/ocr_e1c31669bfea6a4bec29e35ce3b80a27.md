# Improving the performance factors

We said that it is important to build a strong sequential algorithm before we go parallel. We also said that there are parameters such as performance speed-up and efficiency. How can you really measure these variables so that you can determine whether you should parallel or not? If we do go parallel, will the application benefit from it and how significantly?

We will try to answer these questions in topic, and we'll give an example of a built-in Visual Studio compiler feature, which relies on OpenMP, the API developed by Intel in cooperation with Livermore Laboratories from the United States. OpenMP stands for multipiprocessor compilation, which is the Microsoft implementation of the OpenMP API. It is an excellent built feature that supports the native execution by the compiler itself.

First, let's discuss use how we can properly decide whether to use parallelism or not? One way would be by measuring and comparing the execution. Another way would be to prove a certain mathematical formula that is used to represent the application execution in parallel. However, the second approach, if chosen, must also be tested—so again, time measurement is needed.

In order to measure these values, we must bring some variables to the table. If we assume that T(S) is the execution time needed for the sequential algorithm and T(P) is the execution time needed for the parallel algorithm, then we could get the following equation:

```
$I = \frac{T(S)}{T(P)}$
```

In the preceding equation, I stands for improvement. However, we can distinguish the following variations of improvement in the result:

+   - I < 1 indicates a slideshow, which means that the parallel execution will only decrease performances
- I < P indicates a sublinear improvement
- I ~ P indicates a linear improvement
- I > P indicates a superlinear improvement