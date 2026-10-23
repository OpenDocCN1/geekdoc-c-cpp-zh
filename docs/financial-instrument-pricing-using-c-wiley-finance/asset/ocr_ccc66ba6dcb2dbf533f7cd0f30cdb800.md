+   - The value of the reduction’s identity element (0 for addition, 1 for multiplication; for aggregate set union the identity element is the empty set).
+   - The function object that can be applied on a subrange of an iterator range to produce a local partial aggregation. The return value is the local partial result from the first phase of the Parallel Aggregation pattern.
+   - The reduction function that combines the partial results that each subrange has computed.

Answer the following questions:

+   a) Apply this algorithm to the examples in Section 30.4 (for example) and compare it with other aggregation algorithms in that section with regards to efficiency and understandability.
+   b) Determine what the following piece of code is doing:

```
std::vector<long> vec2(2000, 4);
int sumV = 0;
vec2[600] = 4;
auto d = concurrency::parallel_reduce(std::begin(vec2),
std::end(vec2), sumV); std::cout << "Parallel_reduce PPL sum : "
<< d << '\n';
```

How does its performance compare to other aggregation algorithms?

+   c) Compare the performance of PPL aggregation algorithms with that of OpenMP:

```
// OpenMP and reduction variable
M = 8;
std::vector<int> vecA(M, 2);
int sum2 = 0;
int prod2 = 1;
int i;
#pragma omp parallel for private(i), reduction (+ : sum2),
reduction (* : prod2)
for (long i = 0; i < vecA.size(); ++i)
{ // vec is some vector

    sum2 += vecA[i];
    prod2 *= vecA[i];
}
std::cout << "Parallel OpenMP sum and product: "
    << sum2 << ", " << prod2 << '\n';
```

In the case of floating-point data the order in which thread-specific values are combined is non-deterministic in general and hence the final result may not be precisely the same as when the reduction is performed serially. This is caused by the fact that floating-point operations can introduce roundoff errors. This could be a cause of concern in computational finance applications where reproducible and accurate results are needed. We may even decide not to parallelise the specific loop if the error resulting from roundoff becomes unacceptable.

Investigate this anomaly using PPL and OpenMP. Take examples to exhibit the effect of roundoff error.