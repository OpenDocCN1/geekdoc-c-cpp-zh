remember ($9.3.2) to use both a traditional iterator version of a standard-library algorithm and its ranges counterpart, you need to either qualify the call or use a using-declaration

These algorithms, and many more (e.g., $17.3), can be applied to elements of containers, strings, and built-in arrays.

Some algorithms, such as replace() and sort(), modify value elements, but no algorithm adds or subtracts elements of a container. The reason is that a sequence does not identify the container that holds the elements of the sequence. To add or delete elements, you need something that knows about the container (e.g., a back_inserter(); $13.1) or directly refers to the container itself (e.g., push_back() or erase(); $12.2).

Lambdas are very common operations passed as arguments. For example:

Click here to view code image

```
vector<int> v={0,1,2,3,4,5};
for_each(v.begin(),v.end(),[](int &x){x*=x;});
for_each(v.begin(),v.end(),[](int &x){x=sqrt(x);});
```

The standard-library algorithms need to be more carefully designed, and implemented more than the average hand-crafted loop. Know them and use in preference to code written in the bare language.

# 13.6 Parallel Algorithms

When the same task is to do many data items, we can execute it on each data item provided the communications on different data items are independent:

+   * parallel execution: tasks are done on multiple threads (often running on several processor cores)
* vectorized execution: tasks are done on a single thread using vectorization, also known as SIMD ("Single Instruction, Multiple Data").

The standard library offers support for both and we can be specific about wanting sequential execution; in <execution> in namespace execution, we find:

+   * seq: sequential execution (feasible)
* par: parallel execution (feasible)
* unseq: unsequenced (vectorized) execution (is feasible)
* par_unseq: parallel and/or unsequenced execution (is feasible). Consider std::sort()();

Click here to view code image

```
sort(v.begin(),v.end());           // sequential
sort(seq,v.begin(),v.end());      // sequential (same as the default)
sort(par,v.begin(),v.end());        // parallel
sort(par_unseq,v.begin(),v.end());  // parallel and/or vectorized
```

Whether it is worth to parallelize and/vector depends on the algorithm, the number of elements in the sequence, the hardware, and the utilization of hardware by programs running on it. Consequently, the execution policy indicators are just hints. A compiler and/or run-time