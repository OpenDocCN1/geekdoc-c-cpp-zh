A major roadblock for compiler optimization is that certain transformations require semantic knowledge. This is only available for types and operations known to the compiler implementers. The interested reader might also look at a deeper discussion of the topic in [22]. Research is going on to provide user-defined transformations with concept-based optimization [67]. Unfortunately, it will take time for this to become mainstream; even the new Concept extension introduced in C++20 is only a step toward optimization driven by user semantics since it will only deal with syntax at first and semantic concepts can only be emulated (see §5.5).

In the next two sections, we will show user-defined code transformations with meta-programming in the domain of linear algebra. The goal is that the user writes operations as clearly as possible and the function and class templates reach for the maximal achievable performance. Given the Turing completeness of the template system, we can provide any desirable user interface while realizing an implementation underneath that behaves equivalently to the most efficient code, as we will demonstrate in this section. Writing well-tuned templates is a significant programming, testing, and benchmarking effort. For this to pay off, the templates should be contained in well-maintained libraries that are available to a broad user community (at least within the research team or company).

# 5.4.1 Classical Fixed-Size Unrolling

```
=> c++17/fsize_unroll_test.cpp
```

The easiest form of compile-time optimization can be realized for fixed-size data types, in particular for math vectors like those in Section 3.6. Similar to the default assignment, we can write a generic vector assignment:

Click here to view code image

```
template <typename T, int Size>
class fsize_vector
{
public:
    const static int my_size= Size;
    template <typename Vector>
    self& operator=(const Vector& that)
    {
        for (int i= 0; i < my_size; ++i)
```