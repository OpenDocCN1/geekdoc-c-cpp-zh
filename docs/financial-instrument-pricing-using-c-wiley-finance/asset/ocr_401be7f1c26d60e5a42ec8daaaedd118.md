```
// POSIX thread implementation
std::cout << "Native handle:  " << t.native_handle() << '\n';
std::cout << "Number of processors:  "
    << t.hardware_concurrency() << '\n';
}
```

We continue with another example that is more closely related to computational finance. In this case we look at STL algorithms, which we discussed in detail in Chapters 17 and 18, in particular numerical algorithms although the same principles can be applied to other algorithm categories. We take the example of computing the sum and product of the elements of a read-only vector. In this case there is no data race (we introduce the topic of data races in Section 28.7). To this end, we define two lambda functions that encapsulate data and STL algorithms. These functions are then used as input parameters to threads:

```
void STLInThreads(std::size_t n)
{ // Run two algorithms in parallel

    std::vector<double> v(n);
    std::iota(std::begin(v), std::end(v), 1);

    // Sum and product of elements of vector
    // Define lambda functions
    auto sum = [&]()
    { // For vector of length n -> n(n+1)/2

        double initVal = 0.0;  // Must be initialised to a value
        // Add initVal to all elements
        double acc = std::accumulate(v.begin(), v.end(), initVal);
        std::cout << "Sum:  " << acc << std::endl;
    };

    auto product = [&]()
    {
        double initVal = 1.0;
        double acc = std::accumulate(v.begin(), v.end(), initVal,
            std::multiplies<double>());
        std::cout << "Product:  " << acc << std::endl;
    };

    std::thread t1(sum); std::thread t2(product);
    t1.join(); t2.join();
}
```

This code is just one way to improve the speedup of sequential computations. For small arrays the above parallel code may even be slower than the corresponding sequential code and for large arrays the use of reduction variables in OpenMP may be more efficient (or using loop parallelism in PPL, as we shall see in Chapter 30).