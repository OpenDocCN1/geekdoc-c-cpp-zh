As the sample outputs show, scaling and shifting the values produced by nextInt enables the program to simulate rolling a six-sided die. The application uses nested control statements (the switch is nested inside the for) to determine the number of times each side of the die appears. The for statement (lines 21–47) iterates 6,000,000 times. During each iteration, line 23 produces a random value from 1 to 6. That value is then used as the controlling expression (line 26) of the switch statement (lines 26–46). Based on the face value, the switch statement increments one of the six counter variables during each iteration of the loop. When we study arrays in Chapter 7, we’ll show an elegant way to replace the entire switch statement in this program with a single statement! This switch statement has no default case, because we have a case for every possible die value that the expression in line 23 could produce. Run the program, and observe the results. As you’ll see, every time you run this program, it produces different results.

# 6.9.1 Generalized Scaling and Shifting of Random Numbers

Previously, we simulated the rolling of a six-sided die with the statement

```
face = 1 + randomNumbers.nextInt( 6 );
```

This statement always assigns to variable face an integer in the range 1 ≤ face ≤ 6. The width of this range (i.e., the number of consecutive integers in the range) is 6, and the starting number in the range is 1. In the preceding statement, the width of the range is determined by the number 6 that’s passed as an argument to Random method nextInt, and the starting number of the range is the number 1 that’s added to randomNumberGenerator.nextInt(6). We can generalize this result as

```
number = shiftingValue + randomNumbers.nextInt( scalingFactor );
```

where shiftingValue specifies the first number in the desired range of consecutive integers and scalingFactor specifies how many numbers are in the range.

It’s also possible to choose integers at random from sets of values other than ranges of consecutive integers. For example, to obtain a random value from the sequence 2, 5, 8, 11 and 14, you could use the statement

```
number = 2 + 3 * randomNumbers.nextInt( 5 );
```

In this case, randomNumberGenerator.nextInt(5) produces values in the range 0–4. Each value produced is multiplied by 3 to produce a number in the sequence 0, 3, 6, 9 and 12. We add 2 to that value to shift the range of values and obtain a value from the sequence 2, 5, 8, 11 and 14. We can generalize this result as

```
number = shiftingValue +
    differenceBetweenValues * randomNumbers.nextInt( scalingFactor );
```

where shiftingValue specifies the first number in the desired range of values, differenceBetweenValues represents the constant difference between consecutive numbers in the sequence and scalingFactor specifies how many numbers are in the range.

# 6.9.2 Random-Number Repeatability for Testing and Debugging

Class Random’s methods actually generate pseudorandom numbers based on complex mathematical calculations—the sequence of numbers appears to be random. The calculation that produces the numbers uses the time of day as a seed value to change the se-