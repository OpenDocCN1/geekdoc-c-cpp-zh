```
// Generate a random number in the range [0,N-1]
int val = rand() % N;
std::cout << "Random number: " << val << std::endl;
```

The second example generates a random number that uses higher-order bits which are more random than the lower-order bits:

```
// Random number between 1 and 10
int val2 = 1 + int(10.0*rand()/(RAND_MAX + 1.0));
std::cout << "Random number: " << val2 << std::endl;
```

Finally, we execute a simulation to compute the frequency of each generated number in the closed range [0, N−1] (in this case N = 10). We expect the frequencies to be the same for a good random number generator:

```
// Test: generate many random numbers; each number in [0,N-1] should
// occur with equal frequency.
std::vector<std::size_t> histogram(N,0);

std::size_t M = std::numeric_limits<std::size_t>::max();
for (std::size_t i = 1; i <= M; ++i)
{ // Generate random number in [0,N-1] and place in bucket

    val = rand() % N;
    histogram[val]++;
}

for (std::size_t i = 0; i < histogram.size(); ++i)
{ // Print the histogram

    std::cout << "Bucket number: " << i << ", frequency: "
              << histogram[i] << std::endl;
}
```

Typical output in the case of 100 million runs is:

```
Bucket number: 0, frequency: 9994999
Bucket number: 1, frequency: 9996847
Bucket number: 2, frequency: 9998909
Bucket number: 3, frequency: 9999474
Bucket number: 4, frequency: 10001231
Bucket number: 5, frequency: 10005179
Bucket number: 6, frequency: 10004794
Bucket number: 7, frequency: 9998955
Bucket number: 8, frequency: 10000133
Bucket number: 9, frequency: 9999479
```

This completes our discussion of this random number generator. We do not recommend it, especially in conjunction with concurrent calls to rand() or srand() in multithreaded