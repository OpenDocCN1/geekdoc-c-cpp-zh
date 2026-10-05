# Chapter 5. Threads and Shared Memory

```
double ans=0;
#pragma omp parallel for \
reduction(+:ans)
for(long i=0; i < n; i = i+2)
{
    ans += 4.0/(2*i+1);
    ans -= 4.0/(2*i+3);
}
```

Except for lines 2 and 3, this can be a sequential program to sum the Leibniz series. Line 2 is the parallel for construct, which specifies that the for-block extending from lines 4 through 8 must be parallelized. When the program encounters this state, it splits into multiple threads. Each thread will execute a chunk of the iterations of the for-loop.

The reduction clause on line 3 is of much importance. It states that ans is a reduction variable that is tagged +. The compiler understands that each thread should compute its own ans, and the result from all threads should be reduced into a single ans using addition.

An attractive feature of OpenMP is that parallel programs can be written using syntax like that of sequential programs. The programmer is asked to make only minimal adjustments to write parallel programs, although these adjustments can be subtle and their simplicity a major pitfall.

Not every for-loop can be parallelized using the OpenMP parallel for construct. The compiler has to be able to look at the loop and generate the code for the for-loop to be executed by each thread. The for-loops that can be parallelized are said to be in canonical form. The complete definition of for-loops in canonical form is too complicated to be useful for anyone except compiler writers. It is usually possible to tell whether a for-loop is in canonical form by looking.

Even when a for-loop is in canonical form, one has to make sure there are no dependencies between successive iterations of the loop. If the later iterations depend on the execution of an earlier iteration, the loop cannot be parallelized correctly. An example of a for-loop with a dependency across iterations is the following:

```
factorial[0] = 1;
for(int i=1; i < n; i++)
    factorial[i] = i*factorial[i-1];
```