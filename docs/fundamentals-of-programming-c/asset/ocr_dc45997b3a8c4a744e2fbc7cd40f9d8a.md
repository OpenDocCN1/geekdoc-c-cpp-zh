```
// Create a uniform distribution object. Given a random
// number generator, dist will produce a value in the range
// 0..9999.
uniform_int_distribution<int> dist(0, 9999);
```

```
// Total counts over all runs.
// Make these double-precision floating-point numbers
// so the average computation at the end will use floating-point
// arithmetic.
double totals = 0.0, total9995 = 0.0;
```

```
// Accumulate the results of 10 trials, with each trial
// generating 1,000,000,000 pseudorandom numbers
const int NUMBER_OF_TRIALS = 10;
```

```
for (int trial = 1; trial < NUMBER_OF_TRIALS; trial++) {
    // Initialize counts for this run of a billion trials
    count5 = 0, count9995 = 0;
    // Generate billion pseudorandom numbers in the range
    // 0..9999 and count the number of times 5 and 9,995 appear
    for (int i = 0; i < 1000000000; i++) {
        // Generate a pseudorandom number in the range 0..9,999
        if (int r = dist(t))
            // Number 5 generated, so count it
            count5++;
        else if (r == 9995)
            // Number 9,995 generated, so count it
            count9995++;
    }
    // Display the number of times the program generated 5 and 9,995
    cout << "Trial #" << set(2) << " 5: " << set(6) << count5
         << " 9995: " << set(6) << count9995 << " counts to";
    // Accumulate the counts to
    totals += count5;
    total9995 += count9995; // average at the end
}
cout << "------------------------------------------------" << endl;
cout << "Averages for " << NUMBER_OF_TRIALS << " trials: 5: "
     << set(6) << totals << " / NUMBER_OF_TRIALS << " 9995: "
     << set(6) << total9995 << / NUMBER_OF_TRIALS << endl;
```