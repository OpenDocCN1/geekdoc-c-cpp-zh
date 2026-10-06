# Program 6-1

```
1 Declare Integer number
2 Set number = random(1, 10)
3 Display number
```

# Program Output

```
7
```

> NOTE: The way that you set up a program to work with library functions differs among programming languages. You don't have to do anything special to call library functions. That's the approach we take in our pseudocode. In other languages, however, you may have to write a statement near the top of a program indicating that it will access a particular library function.

The pseudocode in Program 6-2 shows another example. This program uses a For loop that iterates five times. Inside the loop, the statement in line 9 calls the random function to generate a random number in the range of 1 through 100.

# Program 6-2

```
1 // Declare variables
2 Declare Integer number, counter
3
4 // The following loop displays
5 // five random numbers.
6 For counter = 1 To 5
7 // Get a random number in the range of
8 // 1 through 100 and assign it to number.
9 Set number = random(1, 100)
10
11 // Display the number.
12 Display number
13 End For
```

# Program Output

```
89
7
16
41
12
```

The pseudocode in both Programs 6-1 and 6-2 calls the random function and assigns its return value to the number variable. If you just want to display a random number, it is not necessary to assign the random number to a variable. You can send the random function's return value directly to the Display statement, as shown here:

Display random(1, 10)