
5. Assuming that each of the following examples is part of a complete program, what will each one print?

```
a. printf("Baa Baa Black Sheep.");
printf("Have you any wool?\n");
```

```
b. printf("Begone!\nO creature of lard!\n");
```

```
c. printf("What?\nNo\nfish?\n");
```

```
d. int num;

num = 2;
printf("%d + %d = %d", num, num, num + num);
```

6. Which of the following are C keywords? main, int, function, char, =

7. How would you print the values of the variables words and lines so they appear in the following form:

```
There were 3020 words and 350 lines.
```

Here, 3020 and 350 represent the values of the two variables.

8. Consider the following program:

```
#include <stdio.h>
int main(void)
{
    int a, b;

    a = 5;
    b = 2;      /* line 7 */
    b = a;      /* line 8 */
    a = b;      /* line 9 */
    printf("%d %d\n", b, a);
    return 0;
}
```

What is the program state after line 7? Line 8? Line 9?

9. Consider the following program:

```
#include <stdio.h>
int main(void)
{
    int x, y;

    x = 10;
    y = 5;      /* line 7 */
y = x + y;    /* line 8 */
x = x*y;      /* line 9 */
printf("%d %d\n", x, y);
return 0;
}
```

What is the program state after line 7? Line 8? Line 9?

## Programming Exercises

Reading about C isn’t enough. You should try writing one or two simple programs to see whether writing a program goes as smoothly as it looks in this chapter. A few suggestions follow, but you should also try to think up some problems yourself. You’ll find answers to selected programming exercises on the publisher’s website.

- 1. Write a program that uses one printf() call to print your first name and last name on one line, uses a second printf() call to print your first and last names on two separate lines, and uses a pair of printf() calls to print your first and last names on one line. The output should look like this (but using your name):
  
  Gustav Mahler ←First print statement
  Gustav          ←Second print statement
  Mahler           ←Still the second print statement
  Gustav Mahler ←Third and fourth print statements

- 2. Write a program to print your name and address.

- 3. Write a program that converts your age in years to days and displays both values. At this point, don’t worry about fractional years and leap years.

- 4. Write a program that produces the following output:
  
  For he’s a jolly good fellow!
  For he’s a jolly good fellow!
  For he’s a jolly good fellow!
  Which nobody can deny!
  
  Have the program use two user-defined functions in addition to main(): one named jolly() that prints the “jolly good” message once, and one named deny() that prints the final line once.

5. Write a program that produces the following output:
Brazil, Russia, India, China
India, China,
Brazil, Russia

Have the program use two user-defined functions in addition to main(): one named br() that prints “Brazil, Russia” once, and one named ic() that prints “India, China” once. Let main() take care of any additional printing tasks.

6. Write a program that creates an integer variable called toes. Have the program set toes to 10. Also have the program calculate what twice toes is and what toes squared is. The program should print all three values, identifying them.

7. Many studies suggest that smiling has benefits. Write a program that produces the following output:
Smile!Smile!Smile!
Smile!Smile!
Smile!

Have the program define a function that displays the string Smile! once, and have the program use the function as often as needed.

8. In C, one function can call another. Write a program that calls a function named one_three(). This function should display the word one on one line, call a second function named two(), and then display the word three on one line. The function two() should display the word two on one line. The main() function should display the phrase starting now: before calling one_three() and display done! after calling it. Thus, the output should look like the following:
starting now:
one
two
three
done!

## Data and C

You will learn about the following in this chapter:

- Keywords:
  `int, short, long, unsigned, char, float, double, _Bool, _Complex, _Imaginary`
- Operator:
  `sizeof`
- Function:
  `scanf()`
- The basic data types that C uses
- The distinctions between integer types and floating-point types
- Writing constants and declaring variables of those types
- How to use the `printf()` and `scanf()` functions to read and write values of different types

Programs work with data. You feed numbers, letters, and words to the computer, and you expect it to do something with the data. For example, you might want the computer to calculate an interest payment or display a sorted list of vintners. In this chapter, you do more than just read about data; you practice manipulating data, which is much more fun.

This chapter explores the two great families of data types: integer and floating point. C offers several varieties of these types. This chapter tells you what the types are, how to declare them, and how and when to use them. Also, you discover the differences between constants and variables, and as a bonus, your first interactive program is coming up shortly.

### A Sample Program

Once again, we begin with a sample program. As before, you’ll find some unfamiliar wrinkles that we’ll soon iron out for you. The program’s general intent should be clear, so try compiling

and running the source code shown in Listing 3.1. To save time, you can omit typing the comments.

### Listing 3.1 The platinum.c Program

```
/* platinum.c -- your weight in platinum */
#include <stdio.h>
int main(void)
{
    float weight;    /* user weight            */
    float value;     /* platinum equivalent    */

    printf("Are you worth your weight in platinum?\n");
    printf("Let's check it out.\n");
    printf("Please enter your weight in pounds: ");

    /* get input from the user                */
    scanf("%f", &weight);
    /* assume platinum is $1700 per ounce     */
    /* 14.5833 converts pounds avd. to ounces troy */
    value = 1700.0 * weight * 14.5833;
    printf("Your weight in platinum is worth $%.2f.\n", value);
    printf("You are easily worth that! If platinum prices drop,\n");
    printf("eat more to maintain your value.\n");

    return 0;
}
```

### Tip Errors and Warnings

If you type this program incorrectly and, say, omit a semicolon, the compiler gives you a syntax error message. Even if you type it correctly, however, the compiler may give you a warning similar to “Warning—conversion from ‘double’ to ‘float,’ possible loss of data.” An error message means you did something wrong and prevents the program from being compiled. A warning, however, means you’ve done something that is valid code but possibly is not what you meant to do. A warning does not stop compilation. This particular warning pertains to how C handles values such as 1700.0. It’s not a problem for this example, and the chapter explains the warning later.

When you type this program, you might want to change the 1700.0 to the current price of the precious metal platinum. Don’t, however, fiddle with the 14.5833, which represents the number of ounces in a pound. (That’s ounces troy, used for precious metals, and pounds avoirdupois, used for people—precious and otherwise.)

Note that “entering” your weight means to type your weight and then press the Enter or Return key. (Don’t just type your weight and wait.) Pressing Enter informs the computer that you have

finished typing your response. The program expects you to enter a number, such as 156, not words, such as too much. Entering letters rather than digits causes problems that require an if statement (Chapter 7, “C Control Statements: Branching and Jumps”) to defeat, so please be polite and enter a number. Here is some sample output:

```
Are you worth your weight in platinum?
Let's check it out.
Please enter your weight in pounds: 156
Your weight in platinum is worth $3867491.25.
You are easily worth that! If platinum prices drop,
eat more to maintain your value.
```

### Program Adjustments

Did the output for this program briefly flash onscreen and then disappear even though you added the following line to the program, as described in Chapter 2, “Introducing C”?

```
getchar();
```

For this example, you need to use that function call twice:

```
getchar();
getchar();
```

The getchar() function reads the next input character, so the program has to wait for input. In this case, we provided input by typing 156 and then pressing the Enter (or Return) key, which transmits a newline character. So scanf() reads the number, the first getchar() reads the newline character, and the second getchar() causes the program to pause, awaiting further input.

### What’s New in This Program?

There are several new elements of C in this program:

- Notice that the code uses a new kind of variable declaration. The previous examples just used an integer variable type (int), but this one adds a floating-point variable type (float) so that you can handle a wider variety of data. The float type can hold numbers with decimal points.
- The program demonstrates some new ways of writing constants. You now have numbers with decimal points.
- To print this new kind of variable, use the %f specifier in the printf() code to handle a floating-point value. The .2 modifier to the %f specifier fine-tunes the appearance of the output so that it displays two places to the right of the decimal.
- The scanf() function provides keyboard input to the program. The %f instructs scanf() to read a floating-point number from the keyboard, and the &weight tells scanf() to
