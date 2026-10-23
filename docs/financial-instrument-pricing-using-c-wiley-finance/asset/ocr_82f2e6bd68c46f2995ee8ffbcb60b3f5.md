then merge these results as a final sequential step. In other words, it performs lock-free thread-local subcomputations during the execution of a parallel algorithm. A data structure is said to be lock free if more than one thread must be able to access the data structure concurrently. It can be used instead of a shared variable and it results in improved performance precisely because there is no contention for the shared variable. This class has default and copy constructors as well as a constructor with a callable object as argument. It also has member functions local() that returns a reference to the thread-private subcomputation and combine() that computes a final value from the set of thread-local computations, as the following code to compute the sum of the elements in a vector shows:

```
// Define the local combiner sum
concurrency::combinable<int> sum3 ([]() { return 0; });

// Compute each local sum
concurrency::parallel_for_each(std::begin(vec),
    std::end(vec), [&sum3, &vec] (std::size_t i)
{
    // Each 'local' is an int
    sum3.local() += vec[i];
});

// Add up local contributions and print it
std::cout << "Parallel PPL (combiner) sum: " <<
    sum3.combine(std::plus<int>()) << '\n';
```

In this case the correct aggregated value will be produced as before. For completeness, we mention how to call other constructors:

```
concurrency::combinable<int> sum4;
concurrency::combinable<int> sum5(sum3);
```

We now discuss the use of PPL aggregation to non-scalar data types. In particular, it can be applied to map/reduce design patterns (see Miner and Shook, 2012) and data analytics applications.

# 30.4.1 An Extended Example: Computing Prime Numbers

We discuss how to compute prime numbers and the distribution of primes as a subset of the positive integers. We discuss both sequential and parallel computation using a combination of PPL, STL, the Boost dynamic bitset library and the C++ std::bitset<T> class. We compare the solutions based on accuracy and performance. We first give a short mathematical introduction to number theory. A prime number (or prime) is a natural number that has no positive divisors other than itself and 1. For example, 5 is prime while 8 is not prime because 1, 2, 4 and 8 are its divisors. A number that is not a prime is called a composite. The property of being prime is called primality. There are several efficient (and not so efficient) algorithms to test for primality. The method that we use here to test the primality of an integer n is called trial division and it consists of dividing n by each integer between 1 and less than or equal to the