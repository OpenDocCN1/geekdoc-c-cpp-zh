```
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

+   - Static Partitioner: this partitioner divides work into a fixed number of ranges. It does not employ work stealing and hence has less overhead. It is optimal to use when each iteration of a parallel loop performs a fixed and uniform amount of work.