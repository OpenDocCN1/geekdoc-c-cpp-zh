
## Review Questions

You'll find answers to the review questions in Appendix A, “Answers to the Review Questions.”

- 1. What is the difference between an actual argument and a formal parameter?
- 2. Write ANSI C function headings for the following functions described. Note we are asking just for the headings, not the body.
  - a. donut() takes an int argument and prints that number of 0s.
  - b. gear() takes two int arguments and returns type int.
  - c. guess() takes no arguments and returns an int value.
  - d. stuff_it() takes a double and the address of a double variable and stores the first value in the given location.
- 3. Write ANSI C function headings for the following functions described. Note that you need write only the headings, not the body.
  - a. n_to_char() takes an int argument and returns a char.
  - b. digits() takes a double argument and an int argument and returns an int.
  - c. which() takes two addresses of double as arguments and returns the address of a double.
  - d. random() takes no argument and returns an int.
- 4. Devise a function that returns the sum of two integers.
- 5. What changes, if any, would you need to make to have the function of question 4 add two double numbers instead?
- 6. Devise a function called alter() that takes two int variables, x and y, and changes their values to their sum and their difference, respectively.
- 7. Is anything wrong with this function definition?

```
void salami(num)
{
    int num, count;

    for (count = 1; count <= num; num++)
        printf("O salami mio!\n");
}
```

**8.** Write a function that returns the largest of three integer arguments.

**9.** Given the following output:

```
Please choose one of the following:
1) copy files             2) move files
3) remove files          4) quit
Enter the number of your choice:
```

- a. Write a function that displays a menu of four numbered choices and asks you to choose one. (The output should look like the preceding.)
- b. Write a function that has two `int` arguments: a lower limit and an upper limit. The function should read an integer from input. If the integer is outside the limits, the function should print a menu again (using the function from part “a” of this question) to reprompt the user and then get a new value. When an integer in the proper limits is entered, the function should return that value to the calling function. Entering a noninteger should cause the function to return the quit value of 4.
- c. Write a minimal program using the functions from parts “a” and “b” of this question. By *minimal*, we mean it need not actually perform the actions promised by the menu; it should just show the choices and get a valid response.

## Programming Exercises

- 1. Devise a function called `min(x,y)` that returns the smaller of two double values. Test the function with a simple driver.
- 2. Devise a function `chline(ch,i,j)` that prints the requested character in columns i through j. Test it in a simple driver.
- 3. Write a function that takes three arguments: a character and two integers. The character is to be printed. The first integer specifies the number of times that the character is to be printed on a line, and the second integer specifies the number of lines that are to be printed. Write a program that makes use of this function.
- 4. The harmonic mean of two numbers is obtained by taking the inverses of the two numbers, averaging them, and taking the inverse of the result. Write a function that takes two double arguments and returns the harmonic mean of the two numbers.
- 5. Write and test a function called `larger_of()` that replaces the contents of two double variables with the maximum of the two values. For example, `larger_of(x,y)` would reset both x and y to the larger of the two.

6. Write and test a function that takes the addresses of three double variables as arguments and that moves the value of the smallest variable into the first variable, the middle value to the second variable, and the largest value into the third variable.

7. Write a program that reads characters from the standard input to end-of-file. For each character, have the program report whether it is a letter. If it is a letter, also report its numerical location in the alphabet. For example, c and C would both be letter 3. Incorporate a function that takes a character as an argument and returns the numerical location if the character is a letter and that returns −1 otherwise.

8. Chapter 6, “C Control Statements: Looping,” (Listing 6.20) shows a power() function that returned the result of raising a type double number to a positive integer value. Improve the function so that it correctly handles negative powers. Also, build into the function that 0 to any power other than 0 is 0 and that any number to the 0 power is 1. (It should report that 0 to the 0 is undefined, then say it’s using a value of 1.) Use a loop. Test the function in a program.

9. Redo Programming Exercise 8, but this time use a recursive function.

10. Generalize the to_binary() function of Listing 9.8 to a to_base_n() function that takes a second argument in the range 2–10. It then should print the number that is its first argument to the number base given by the second argument. For example, to_base_n(129,8) would display 201, the base-8 equivalent of 129. Test the function in a complete program.

11. Write and test a Fibonacci() function that uses a loop instead of recursion to calculate Fibonacci numbers.

## Arrays and Pointers

You will learn about the following in this chapter:

- Keyword:
  `static`
- Operators:
  `&` `*` (unary)
- How to create and initialize arrays
- Pointers (building on the basics you already know) and see how they relate to arrays
- Writing functions that process arrays
- Two-dimensional arrays

People turn to computers for tasks such as tracking monthly expenses, daily rainfall, quarterly sales, and weekly weights. Enterprises turn to computers to manage payrolls, inventory, and customer transactions. As a programmer, you inevitably have to deal with large quantities of related data. Often, arrays offer the best way to handle such data in an efficient, convenient manner. Chapter 6, “C Control Statements: Looping,” introduced arrays, and this chapter takes a more thorough look. In particular, it examines how to write array-processing functions. Such functions enable you to extend the advantages of modular programming to arrays. In doing so, you can see the intimate relationship between arrays and pointers.

## Arrays

Recall that an *array* is composed of a series of elements of one data type. You use *declarations* to tell the compiler when you want an array. An *array declaration* tells the compiler how many elements the array contains and what the type is for these elements. Armed with this information, the compiler can set up the array properly. Array elements can have the same types as ordinary variables. Consider the following example of array declarations:

```
/* some array declarations */
int main(void)
```

## Listing 10.1 The day_mon1.c Program

```
/* day_mon1.c -- prints the days for each month */
#include <stdio.h>
#define MONTHS 12

int main(void)
{
    int days[MONTHS] = {31,28,31,30,31,30,31,31,30,31,30,31};
    int index;

    for (index = 0; index < MONTHS; index++)
        printf("Month %d has %2d days.\n", index +1,
            days[index]);

    return 0;
}
```

The output looks like this:

```
Month  1 has 31 days.
Month  2 has 28 days.
Month  3 has 31 days.
Month  4 has 30 days.
Month  5 has 31 days.
Month  6 has 30 days.
Month  7 has 31 days.
Month  8 has 31 days.
Month  9 has 30 days.
Month 10 has 31 days.
Month 11 has 30 days.
Month 12 has 31 days.
```

Not quite a superb program, but it’s wrong only one month in every four years. The program initializes days[] with a list of comma-separated values enclosed in braces.

Note that this example used the symbolic constant MONTHS to represent the array size. This is a common and recommended practice. For example, if the world switched to a 13-month calendar, you just have to modify the #define statement and don’t have to track down every place in the program that uses the array size.

## Note Using const with Arrays

Sometimes you might use an array that’s intended to be a read-only array. That is, the program will retrieve values from the array, but it won’t try to write new values into the array. In such cases, you can, and should, use the const keyword when you declare and initialize the array. Therefore, a better choice for Listing 10.1 would be

```
const int days[MONTHS] = {31,28,31,30,31,30,31,31,30,31,30,31};
```
