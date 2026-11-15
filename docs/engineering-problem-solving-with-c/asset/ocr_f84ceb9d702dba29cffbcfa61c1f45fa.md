```
int main()
{
   // Declare objects.
   unsigned int seed;

   // Get seed value from the user.
   cout << "Enter a positive integer seed value: \\n";
   cin >> seed;
   srand(seed); // Seed random number generator.

   // Generate and print ten random numbers.
   cout << "Random Numbers: \\n";
   for (int k = 1; k <= 10; ++k)
   {
      cout << rand() << ' '; //Print a random number.
   }

   cout << endl;
   // Exit program.
   return 0;
}
/*--------------------------------------------------------------*/
```

A sample output follows, using g++ on a Linux system:

```
Enter a positive integer seed value:
123
Random Numbers:
128959393 169290103 436085873 748533630 776550279 289139331
807385195 556889022 95168426 188844001
```

Experiment with the program on your computer system; use the same seed to generate the same numbers, and use different seeds to generate different numbers.

Because the prototype statements for rand() and srand() are included in cstdlib, we do not need to include them separately in a program. However, it is instructive to analyze these prototype statements. Because the rand() function returns an integer and has no input, its prototype statement is

```
int rand();
```

Because the srand() function returns no value and has an unsigned integer as an argument, its prototype statement is

```
void srand(unsigned int);
```

Generating random integers over a specified range is simple to do with the rand() function. For example, suppose that we want to generate random integers between 0 and 7. The following statement first generates a random number that will be between 0 and RAND_MAX and then uses the modulus operator to compute the modulus of the random number and the integer 8:

```
x = rand() % 8;
```