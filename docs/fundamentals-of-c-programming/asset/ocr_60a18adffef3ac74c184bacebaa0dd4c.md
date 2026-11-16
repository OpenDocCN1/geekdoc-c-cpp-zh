```
// Verify the largest number that rand can produce
std::cout << "RAND_MAX = " << RAND_MAX << '\n';

// Total counts over all the runs.
// Make these double-precision floating-point numbers
// so the average computation at the end will use floating-point
// arithmetic.
double total5 = 0.0, total9995 = 0.0;

// Accumulate the results of 10 trials, with each trial
// generating 1,000,000,000 pseudorandom numbers
const int NUMBER_OF_TRIALS = 10;

for (int trial = 1; trial <= NUMBER_OF_TRIALS; trial++) {
  // Initialize counts for this run of a billion trials
  int count5 = 0, count9995 = 0;
  // Generate one billion pseudorandom numbers in the range
  // 0..9,999 and count the number of times 5 and 9,995 appear
  for (int i = 0; i < 1000000000; i++) {
    // Generate a pseudorandom number in the range 0..9,999
    int r = rand() % 10000;
    if (r == 5)
      count5++;
    else if (r == 9995)
      count9995++;
  }
  // Display the number of times the program generated 5 and 9,995
  std::cout << "Trial #" << trial << ": " << std::setw(2) << "trial < " " 5: " << count5
            << " 9995: " << count9995 << '\n';
  total5 += count5;
  total9995 += count9995; // average them at the end
}
std::cout << "\n\n";
std::cout << "Averages for " << NUMBER_OF_TRIALS << " trials: 5: "
          << total5 / NUMBER_OF_TRIALS << " 9995: "
          << total9995 / NUMBER_OF_TRIALS << '\n';
}
```

The output of Listing 13.9 (badrand.cpp) shows that our pseudorandom number generator favors 5 over 9.995:

| RAND_MAX = 32767 |
| Trial # 1: 5 122295 9995: 91255 |
| Trial # 2: 5 121789 9995: 91862 |
| Trial # 3: 5 122440 9995: 91228 |
| Trial # 4: 5 121602 9995: 91877 |
| Trial # 5: 5 122599 9995: 91378 |
| Trial # 6: 5 121599 9995: 91830 |
| Trial # 7: 5 122366 9995: 91598 |
| Trial # 8: 5 121839 9995: 91387 |
| Trial # 9: 5 122295 9995: 91608 |
| Trial #10: 5 121898 9995: 91519 |
| Averages for 10 trials: 5: 122072 9995: 91554.2 |