would be an error since we disabled the function for lvalue arguments. Recent compilers will tell us that about the SFINAE-based disabling while older compilers just claim the miss of an overload (or fail to compile the anonymous type parameter).

Of course, we can declare everything to be an rvalue with std::move and shoot ourselves in the foot with such a lie. Instead, we should create an anonymous copy like

```
auto B = normalize(lu(permute(clone(A))));
```

Here, we first create a copy of A and all transformations are performed on this copy. The same copy is finally taken over by the move constructor of B. Altogether, we only created one single copy of A whose transformed data is finally kept in B.

# A.9.5 Benchmark Sources of Dynamic Unrolling

```
=> c++11/vector_unroll_example.cpp
```

The following program was used for benchmarking in Section 5.4.3:

```
#include <iostream>
#include <chrono>
// ...

using namespace std::chrono;

template <typename TP>
double duration_ms(TP const& from, const TP& to, unsigned rep)
{
    return duration_cast<nanoseconds>((to - from) / rep).count() / 1000.;
}

int main()
{
    unsigned s = 1000;
    if (argc > 1) s = atoi(argv[1]); // read (potentially)
    // from command line
    vector<float> u(s), v(s), w(s);
    vector<float> u(s), v(s), w(s);

    for (unsigned i = 0; i < s; ++i) {
        v[i] = float(i);
        w[i] = float(2*i + 15);
    }

    // Load to L1 or L2 cache
    for (unsigned j = 0; j < 3; j++)
        for (unsigned i = 0; i < s; ++i)
            u[i] = 3.0f * v[i] + w[i];

    const unsigned rep = 200000;
```