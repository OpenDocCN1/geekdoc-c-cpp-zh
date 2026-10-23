
If an exception is thrown by one of the work functions then it will be deferred and rethrown when all tasks finish. In the case of multiple exceptions being thrown the runtime chooses one of the exceptions to be rethrown. The remaining exceptions will not be externally observed. We simulate an application of tasks in which exceptions are thrown:

```
// Functions throwing exceptions
void exception1()
{
    throw -1;
}

void exception2()
{
    throw 'Z';
}

// Parallel invoke with exceptions
try
{
    concurrency::parallel_invoke(
        [&]() { exception1(); },
        []() { f1(); },
        [&]() { exception2(); }
    );
}
catch (int& e)
{
    std::cout << "\ninteger exception " << e << '\n';
}
catch (char& e)
{
    std::cout << "\ncharacter exception " << e << '\n';
}
```

You can run this code and see what happens.

We can reproduce the functionality of parallel_invoke by creating a task group and calling its run and wait methods. The first example is:

```
// Parallel task using task group
concurrency::task_group tg;

tg.run([]() { f2(); });
tg.run([]() { f1(); });
tg.wait();
```

It is also possible to combine the run and wait methods into a single operation:

```
// Parallel task using task group
concurrency::task_group tg2;

std::cout << "* Run and wait combined\n";
tg2.run([]() { f2(); });
tg2.run_and_wait([]() { f1(); });
```

The run_and_wait method acts as a hint to the scheduler that it can reuse the current context to execute the new task.

## 30.2.4 Parallel Transform and Parallel Reduction

These useful algorithms are the parallel versions of the STL algorithms `std::transform` and `std::accumulate`, respectively. They support random access, bidirectional and forward iterators.

We give examples and for completeness we also give the code in the sequential case:

```
std::vector<double> v1 = { 1.0, 2.0, 3.0, 4.0};

// Sequential transform
// Modifier, predefined function objects
std::transform(v1.begin(), v1.end(), v1.begin(),
               std::negate<double>());
print(v1, std::string("Negated values: "));

std::transform(v1.begin(), v1.end(), v1.begin(),
               [](double d) { return -d; });
print(v1, std::string("Negated values: "));

// Parallel transform
auto MyNegate = [](double d) { return - d; };
concurrency::parallel_transform(std::begin(v1), std::end(v1),
                                std::begin(v1), MyNegate);
print(v1, std::string("Negated values: "));

// Reduce
double initVal = 0.0;
std::cout << concurrency::parallel_reduce(std::begin(v1),
                                          std::end(v1), initVal) << '\n';

double acc1 = std::accumulate(std::begin(v1), std::end(v1), initVal);
std::cout << "Sum , classic sum: " << acc1 << std::endl;
```

## 30.3 PARTITIONING WORK

In general, we improve the performance of algorithms that operate on a container by partitioning its index space into ranges and then assigning each range to a thread. In other words, we distribute consecutive chunks of data between threads. We can manually perform this partitioning but the end result is not scalable. Nonetheless, it is instructive to write user-defined code to get a feeling for how PPL works. Furthermore, you will need to hand-craft a solution because C++ does not support *automatic partitioning* at the moment of writing. To this end, we discuss an example of the *Divide and Conquer* parallel design pattern (Mattson, Sanders and Massingill, 2005) applied to the sorting of a sequential container. We split the problem into a number of smaller subproblems, solve each one independently and then merge the subsolutions into a solution for the whole problem. We discuss a user-defined quicksort algorithm with three implementations, namely sequential C++, C++ threads and PPL’s parallel_invoke. First, the sequential version is:

```
template <typename ForwardIt>
    void QuickSort(ForwardIt first, ForwardIt last)
{ // Sequential recursive implementation of Hoare's Quicksort algorithm

    // Base case for recursion
    if (first == last) return;

    // Get value at given distance std::distance(first, last) / 2
                                    // from first
    auto pivot = *std::next(first, std::distance(first, last) / 2);

    // Move elements in [first,last] to front for t < pivot value
    ForwardIt middle1
        = std::partition(first, last, [pivot](const auto& t)
        { return t < pivot; });
    // Move elements in [middle,last] to front for t >= pivot value
    ForwardIt middle2
        = std::partition(middle1, last, [pivot](const auto& t)
        { return pivot >= t; });

    QuickSort(first, middle1);
    QuickSort(middle2, last);
}
```

For the C++ case we create two threads and then merge their separate results:

```
template <typename T>
    void MergeSort(std::list<T>& con)
{ // Parallel mergesort

    // 1. Split container into two pieces
    // 2. Quicksort the pieces
    // 3. Merge the pieces

    auto first = std::begin(con); auto last = std::end(con);
    if (first == last) return;

    auto pivot = std::next(first, std::distance(first, last) / 2);

    auto fn = [](auto f, auto s) {QuickSort(f, s); };

    std::thread t1(fn,first, pivot);
    std::thread t2(fn, pivot, last);

// Wait on t1 and t2
t1.join();
t2.join();

// Clumsy code; slows things down somewhat
std::list<T> result;
std::merge(first, pivot, pivot, last, std::back_inserter(result));
con = std::move(result);
}
```

The PPL solution is:

```
template <typename T>
void MergeSortPPL(std::list<T>& con)
{ // Parallel mergesort

// 1. Split container into two pieces
// 2. Quicksort the pieces
// 3. Merge the pieces

auto first = std::begin(con); auto last = std::end(con);
if (first == last) return;

auto pivot = std::next(first, std::distance(first, last) / 2);

concurrency::parallel_invoke(
    [&first, &pivot]() {QuickSort(first, pivot); },
    [&pivot, &last]() {QuickSort(pivot, last); }
);

// Clumsy code; slows things down somewhat
std::list<T> result;
std::merge(first, pivot, pivot, last, std::back_inserter(result));
con = std::move(result);
}
```

The reason for creating this code is to show how to partition a problem into subproblems and solve each subproblem. In general, we (and probably most developers) do not have the time to build production software for these kinds of problems and prefer to use a library such as PPL or TBB. In particular, PPL’s parallel_for, parallel_for_each and parallel_transform algorithms provide overloaded versions that take an extra parameter called a partitioner that defines how work is divided. The default partitioning mechanism creates an initial workload and then uses a work-stealing algorithm and range-stealing algorithm to balance the partitions when the workloads become unbalanced.

There are four partitioning options:

- Static Partitioner: this partitioner divides work into a fixed number of ranges. It does not employ work stealing and hence has less overhead. It is optimal to use when each iteration of a parallel loop performs a fixed and uniform amount of work.
- **Affinity Partitioner:** this partitioner divides work into a fixed number of ranges. It is similar to a static partitioner but it improves *cache affinity* (moves the threads of a workload closer together) because of the way it maps ranges to worker threads.
- **Auto Partitioner:** this partitioner divides work into an initial number of ranges. The runtime uses this number as default. Each range can be divided into subranges, thus allowing load balancing to occur. The runtime redistributes subranges of work from other threads to that thread.
- **Simple Partitioner:** this partitioner divides work into ranges such that each range has at least the number of iterations that are specified by a given *chunk size*. This choice supports load balancing. However, the runtime does not divide ranges into subranges.

We give an example:

```
// Partitioners
auto negate = [] (double d) { return -d; };

concurrency::static_partitioner stap;
concurrency::simple_partitioner simp(4); // Chunk size
concurrency::auto_partitioner autp;
concurrency::affinity_partitioner affp;

std::vector<double> v(10'000'000);
concurrency::parallel_transform(v.begin(), v.end(), v.begin(), negate, stap);
concurrency::parallel_transform(v.begin(), v.end(), v.begin(), negate, simp);
concurrency::parallel_transform(v.begin(), v.end(), v.begin(), negate, autp);
concurrency::parallel_transform(v.begin(), v.end(), v.begin(), negate, affp);
```

We conclude this section with the remark that the type of application and its workload will determine which partitioner to use in a given context. It is recommended that you conduct experiments to determine which option is most suitable for your application.

### 30.3.1 Parallel Sort

PPL has support for three sorting algorithms:

- **Parallel Sort:** this is a general *compare-based* algorithm meaning that elements are compared by value. It has no additional memory requirements and is suitable for general-purpose sorting.
- **Parallel Buffered Sort:** this is a compare-based algorithm. It performs better than the general parallel sort algorithm but requires an additional *O(N)* space.
- **Radix Sort:** this is a *hash-based* algorithm because it uses keys to sort elements. We can compute the destination of an element instead of having to use comparison operations. It requires an additional *O(N)* space.

An example is:

```
void ParallelSort()
{ // Sorting in PPL
```
