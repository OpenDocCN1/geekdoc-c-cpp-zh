Listing 11-8 uses a nested for loop to generate 100 random values. The rand() function in Line 13 generates the values. The printf() function in Line 14 displays the values by using the %d conversion character, which outputs int values.

Exercise 11-17: Type the source code shown in Listing 11-8 into your editor. Save, build, and run to behold 100 random values.

Exercise 11-18: Modify the code so that all values displayed are in the range 0 through 20.

![](bbox=[0.18, 0.35, 0.26, 0.48])

Here's a hint for Exercise 11-18: Use the modulus assignment operator to limit the range of the random numbers. The format looks like this:

```
r%=n;
```

r is the number returned from the rand() function. %= is the modulus assignment operator. n is the range limit, plus 1. After the preceding statement, values returned are in the range 0 through n-1. So if you want to generate values between 1 and 100, you would use this formula:

```
value = (r % 100) + 1;
```

# Making the numbers more random

Just to give some credit to the snooty mathematicians who claim that computers generate pseudo-random numbers, run the program you generated from Exercise 11-18. Observe the output. Run the program again. See anything familiar?

The rand() function is good at generating a slew of random values, but they're predictable values. To make the output less predictable, you need to seed the random-number generator. That's done by using the srand() function.

Like the rand() function, the srand() function requires the stdlib.h header, shown at Line 2 in Listing 11-9. The function requires an unsigned int value, seed, which is declared at Line 6. The scanf() function at Line 10 reads in the unsigned value by using the %u placeholder. Then the srand() function uses the seed value in Line 11.