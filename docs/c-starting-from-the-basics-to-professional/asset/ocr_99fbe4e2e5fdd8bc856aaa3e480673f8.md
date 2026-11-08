```
while (count < max)
{
    bool isprime {true};    // Indicates when a prime is found

    const auto limit = static_cast<unsigned>(std::sqrt(trial));
    for (size_t i {}; primes[i] <= limit && isprime; ++i)
    {
        isprime = trial % primes[i] > 0;    // False for exact division
    }

    if (isprime)                        // We got one...
        primes[count++] = trial;         // ...so save it in primes array

    trial += 2;                          // Next value for checking
}

// Output primes 10 to a line
for (size_t i {}; i < max; ++i)
{
    std::cout << std::format("{:10}", primes[i]);
    if ((i + 1) % 10 == 0)              // After every 10th prime...
        std::cout << std::endl;          // ...start a new line
}
std::cout << std::endl;

delete[] primes;                         // Free up memory...
primes = nullptr;                        // ...and reset the pointer
```

The output is essentially the same as the previous program, so we won’t reproduce it here. Overall, the program is similar but not the same as the previous version. After reading the number of primes required from the keyboard and storing it in max, you allocate an array of that size in the free store using the new operator. The address that’s returned by new is stored in the pointer, primes. This will be the address of the first element of an array of max elements of type unsigned (int).

Unlike Ex06_05, all statements and expressions involving the primes array in this program use the array notation. But only because this is easier; you could equally well use and write them using pointer notation: *primes = 2, *(primes + i), *(primes + count++) = trial, and so on.

Before allocating the primes array and inserting the first prime, 2, we verify that the user did not enter the number zero. Without this safety measure, the program would otherwise write the value 2 into a memory location beyond the bounds of the allocated array, which would have undefined and potentially catastrophic results.

Notice also that the determination of whether a candidate is prime is improved compared to Ex6_05.cpp. Dividing the candidate in trial by existing primes ceases when primes up to the square root of the candidate have been tried, so finding a prime will be faster. The sqrt() function from the <cmath> header does this.

When the required number of primes has been output, you remove the array from the free store using the delete[] operator, not forgetting to include the square brackets to indicate that it’s an array you’re deleting. The next statement resets the pointer. It’s not essential here, but it’s good to get into the habit of always resetting a pointer after freeing the memory to which it points; it could be that you add code to the program at a later date.