
## CHAPTER 9 Value-Returning Functions

the rand function. The first sample value for Example 1 is 27. When processing the 1 + 27 % (6 - 1 + 1) expression, the computer evaluates the part of the expression within parentheses; in this case 6 - 1 + 1 evaluates to 6. The expression now becomes 1 + 27 % 6. The modulus operator (%) tells the computer to divide 27 by 6 and then find the remainder; in this, the remainder is 3. The expression now becomes 1 + 3. In other words, the expression in Example 1 evaluates to the integer 4 when the rand value is 27. As Figure 9-18 indicates, the expression will evaluate to the integers 3 and 4 when the rand value is 8 and 32, respectively, and within the range of one through six. Now consider the sample value used in Example 2: the first sample value is 32. When processing 10 + 32 % (100 - 1 + 1) expression, the computer evaluates the first part of the expression within parentheses; in this case 100 - 1 + 1 evaluates to 100. The expression now becomes 10 + 32 % 91. The modulus operator (%) tells the computer to divide 32 by 91 and then find the remainder; in this case, the remainder is 79. The expression now becomes 10 + 79. Finally, the computer adds 10 to the number 79, giving 89. Therefore, the expression in Example 2 evaluates to the integer 89 when the rand value is 32. The expression evaluates to the integers 14 and 53 when the rand value is 4 and 2500, respectively. Notice that, in this case, the three random integers (89, 14, and 53) are within the range of 1 through 100.

Recall from Chapter 4 the modulus operator divides two integers and returns the remainder as an integer.

You can write the expressions in Figure 9-8 as rand() % 6 + 10. Including the lowerBound and upperBound values within the parentheses makes the expression clearer and more documenting.

> HOW TO Generate Random Integers within a Specific Range
> lowerBound + rand() % (upperBound – lower + 1)

Example 1
> out << 1 + rand() % (6 - 1 + 1);
> displays a random integer from 1 to 6 on the computer screen

| rand value: 8 | 1 + 27 % (6 - 1 + 1) |
| :--- | :--- |
| 6 - 1 is evaluated first and results in 6 | 1 + 27 % 6 |
| 27 % 6 is evaluated next and results in 3 | 1 + 3 |
| 1 + 3 is evaluated last and results in 4 | 4 |
| rand value: 8 | 1 + 8 % (6 - 1 + 1) |
| 6 - 1 is evaluated first and results in 6 | 1 + 8 % 6 |
| 8 % 6 is evaluated next and results in 2 | 1 + 2 |
| 1 + 2 is evaluated last and results in 3 | 3 |
| rand value: 324 | 1 + 324 % (6 - 1 + 1) |
| 6 - 1 is evaluated first and results in 6 | 1 + 324 % 6 |
| 324 % 6 is evaluated next and results in 0 | 1 + 0 |
| 1 + 0 is evaluated last and results in 1 | 1 |

Figure 9-8 How to generate random integers within a specific range (continues)

### Example 2

```cpp
int num = 0;
num = 10 + rand() % (100 - 10 + 1);
// assign a random integer from 10 to 100 to the variable
```

| rand value: 352 | 10 + 352 % (100 - 10 + 1) |
| :--- | :--- |
| 100 - 10 is evaluated first and results in 91 | 10 + 352 % 91 |
| 352 % 91 is evaluated and results in 79 | 10 + 79 |
| 10 + 79 is evaluated last and results in 89 | 89 |

| rand value: 4 | 10 + 4 % (100 - 10) |
| :--- | :--- |
| 100 - 10 is evaluated first and results in 91 | 10 + 4 % 91 |
| 4 % 91 is evaluated and results in 14 | 10 + 4 |
| 10 + 4 is evaluated last and results in 14 | 14 |

| rand value: 2500 | 10 + 2500 % (100 - 10) |
| :--- | :--- |
| 100 - 10 is evaluated first and results in 91 | 10 + 2500 % 91 |
| 2500 % 91 is evaluated and results in 43 | 10 + 43 |
| 10 + 43 is evaluated last and results in 53 | 53 |

**Figure 9-8** *How to generate random integers within a specific range*

You initialize the random number generator in each program that it is used. Otherwise, it will generate the same series of numbers each time the program is executed. Typically, the initialization task is performed at the beginning of the program. You initialize the random number generator using the **srand** function. *Like* the **rand** function, the **srand** function is a built-in C++ function. *However*, unlike the **rand** function is a void function, which means it does not return a value. You will learn more about functions in Chapter 10. Figure 9-9 shows the syntax of the **srand** function and includes examples of using the function. The *actual argument* in the syntax represents the starting point for the random number generator. The computer uses the starting point (or seed) in the mathematical algorithm it employs when selecting the random numbers. If you use the same seed, as shown in Example 1 Figure 9-7. *However*, a more common way to initialize the random number generator is to use the current time. The actual argument in the syntax represents the starting point for the random number generator. The computer uses the starting point (or seed) in the mathematical algorithm it employs when selecting the random numbers. If you use the same seed, as shown in Example 1 Figure 9-7. *However*, a more common way to initialize the random number generator is to use the current time. The actual argument in the syntax represents the starting point for the random number generator. The computer uses the starting point (or seed) in the mathematical algorithm it employs when selecting the random numbers. If you use the same seed, as shown in Example 1 Figure 9-7. *However*, a more common way to initialize the random number generator is to use the current time. The actual argument in the syntax represents the starting point for the random number generator. The computer uses the starting point (or seed) in the mathematical algorithm it employs when selecting the random numbers. If you use the same seed, as shown in Example 1 Figure 9-7. *However*, a more common way to initialize the random number generator is to use the current time. The actual argument in the syntax represents the starting point for the random number generator. The computer uses the starting point (or seed) in the mathematical algorithm it employs when selecting the random numbers.

### CHAPTER 9 Value-Returning Functions

### HOW TO Generate Random Integers within a Specific Range
> lowerBound + rand() % (upperBound – lower + 1)

Example 1
> out << 1 + rand() % (6 - 1 + 1);
> displays a random integer from 1 to 6 on the computer screen

### Example 2
```cpp
int num = 0;
num = 10 + rand() % (100 - 10 + 1);
// assign a random integer from 10 to 100 to the variable
```

### HOW TO use srand
Syntax
> srand(seed)

Example 1
```cpp
int x = 0;
srand(time(0));
cout << x;
```

Example 2
```cpp
int randNum = 0;
srand(time(0));
cout << randNum;
```

Example 3
```cpp
int randNum = 0;
srand(time(0));
cout << randNum;
```

### Figure 9-9 How to use srand

### Figure 9-10 IPO chart information for random addition

| Input | Processing | Output |
| :--- | :--- | :--- |
| user's answer | 1. initialize the random number generator | |
| | 2. repeat (counter from 1 to 5) | |
| | - generate the first random number | |
| | - generate the second random number | |
| | - calculate the correct answer by adding together the first and second random number | |
| | - display the addition problem | |
| | - enter the user's answer | |
| | - if (user's answer matches correct) | |
| | - display "Correct!" message | |
| | - display "Sorry, the answer is " message followed by the correct answer and a period | |
| | - display two blank lines | |

### Algorithm
1. initialize the random number generator
2. repeat (counter from 1 to 5)
   - generate the first random number
   - generate the second random number
   - calculate the correct answer by adding together the first and second random number
   - display the addition problem
   - enter the user's answer
   - if (user's answer matches correct)
     - display "Correct!" message
     - display "Sorry, the answer is " message followed by the correct answer and a period
   - display two blank lines

