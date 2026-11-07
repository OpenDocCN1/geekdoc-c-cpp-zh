```
```c
long long int fibonacci(int n); // function prototype

int main(void) {
    puts("Sequential calls to fibonacci(50) and fibonacci(49)");

    // calculate fibonacci value for 50
    time_t startTime1 = time(NULL);
    puts("Calculating fibonacci(50)");
    long long int result1 = fibonacci(50);
    time_t endTime1 = time(NULL);

    printf("fibonacci(50) = %llu\n", result1);
    printf("Calculation time = %f minutes\n",
           difftime(endTime1, startTime1) / 60.0);

    time_t startTime2 = time(NULL);
    puts("Calculating fibonacci(49)");
    long long int result2 = fibonacci(49);
    time_t endTime2 = time(NULL);

    printf("fibonacci(49) = %llu\n", result2);
    printf("Calculation time = %f minutes\n",
           difftime(endTime2, startTime2) / 60.0);

    printf("Total calculation time = %f minutes\n",
           difftime(endTime2, startTime1) / 60.0);
}

// Recursively calculates fibonacci numbers
long long int fibonacci(int n) {
    if (0 == n || 1 == n) { // base case
        return n;
    }
    else { // recursive step
        return fibonacci(n - 1) + fibonacci(n - 2);
    }
}
```
```

# d) Run on a Docker Container with One Core

```
```text
Sequential calls to fibonacci(50) and fibonacci(49)
Calculating fibonacci(50)
fibonacci(50) = 12586269025
Calculation time = 1.700000 minutes

Calculating fibonacci(49)
fibonacci(49) = 7778742049
Calculation time = 1.050000 minutes

Total calculation time = 2.750000 minutes
```
```

**Fig. C.5** | Fibonacci calculations performed sequentially. (Part 2 of 3.)