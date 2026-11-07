```
~~~cpp
int main() {
    // set up random-number generation
    std::random_device rd;
    std::default_random_engine eng(rd());
    std::uniform_int_distribution ints{0, 1000};

    std::cout << "Creating vectors\n";
    std::vector<int> v1(100'000'000);
    std::vector<int> v2(1'000'000'000);

    std::cout << "Filling vectors with random ints\n";
    std::generate(std::execution::par, v1.begin(), v1.end(),
                  [&]() { return ints(eng); });
    std::generate(std::execution::par, v2.begin(), v2.end(),
                  [&]() { return ints(eng); });

    std::cout << "\nCalculating square roots:\n";

    // time the transforms on 100,000,000 elements
    std::cout << std::format("{} elements with par\n", v1.size());
    double parTime1{timeTransform(std::execution::par, v1)};
    std::cout << std::format("{} elements with unseq\n", v1.size());
    double unseqTime1{timeTransform(std::execution::unseq, v1)};

    // time the transforms on 1,000,000,000 elements
    std::cout << std::format("{} elements with par\n", v2.size());
    double parTime2{timeTransform(std::execution::par, v2)};
    std::cout << std::format("{} elements with unseq\n", v2.size());
    double unseqTime2{timeTransform(std::execution::unseq, v2)};

    // display table of timing results
    std::cout << "\nExecution times (in seconds):\n\n"
              << std::format("{:>13} {:>17} {:>21}\n", "# of elements",
                              "par (parallel)", "unseq (vectorized)")
              << std::format("{:>13} {:>17.3f} {:>21.3f}\n",
                              v1.size(), parTime1, unseqTime1)
              << std::format("{:>13} {:>17.3f} {:>21.3f}\n",
                              v2.size(), parTime2, unseqTime2);
}
~~~
```

```
~~~
Creating vectors
Filling vectors with random ints

Calculating square roots:
100000000 elements with par
100000000 elements with unseq
1000000000 elements with par
1000000000 elements with unseq

Execution times (in seconds):
~~~
```

| # of elements | par (parallel) | unseq (vectorized) |
| ---: | ---: | ---: |
| 100000000 | 2.401 | 1.215 |
| 1000000000 | 22.969 | 11.787 |

**Fig. 17.2** | Performing transforms with execution policies par and unseq. (Part 2 of 2.)