
8. What is a linker error? Give three examples.
9. What is a logic error? Give three examples.
10. List four potential sources of program errors discussed in the text.
11. How do you know if a result is plausible? What techniques do you have to answer such questions?
12. Compare and contrast having the caller of a function handle a run-time error vs. the called function’s handling the run-time error.
13. Why is using exceptions a better idea than returning an “error value”?
14. How do you test if an input operation succeeded?
15. Describe the process of how exceptions are thrown and caught.
16. Why, with a **vector** called **v**, is **v[v.size()]** a range error? What would be the result of calling this?
17. Define *pre-condition* and *post-condition*; give an example (that is not the **area()** function from this chapter), preferably a computation that requires a loop.
18. When would you *not* test a pre-condition?
19. When would you *not* test a post-condition?
20. What are the steps in debugging a program?
21. Why does commenting help when debugging?
22. How does testing differ from debugging?

## Terms

- argument error
- exception
- requirement
- assertion
- invariant
- run-time error
- catch
- link-time error
- syntax error
- compile-time error
- logic error
- testing
- container
- post-condition
- **throw**
- debugging
- pre-condition
- type error
- error
- range error

## Exercises

1. If you haven’t already, do the **Try this** exercises from this chapter.
2. The following program takes in a temperature value in Celsius and converts it to Kelvin. This code has many errors in it. Find the errors, list them, and correct the code.

```cpp
double ctok(double c)      // converts Celsius to Kelvin
{
    int k = c + 273.15;
    return int
}

int main()
{
    double c = 0;        // declare input variable
    cin >> d;           // retrieve temperature to input variable
    double k = ctok("c");  // convert temperature
    Cout << k << '/n';  // print out temperature
}
```

3. Absolute zero is the lowest temperature that can be reached; it is −273.15°C, or 0K. The above program, even when corrected, will produce erroneous results when given a temperature below this. Place a check in the main program that will produce an error if a temperature is given below −273.15°C.

4. Do exercise 3 again, but this time handle the error inside `ctok()`.

5. Add to the program so that it can also convert from Kelvin to Celsius.

6. Write a program that converts from Celsius to Fahrenheit and from Fahrenheit to Celsius (formula in §4.3.3). Use estimation (§5.8) to see if your results are plausible.

7. Quadratic equations are of the form $ a \cdot x^{2} + b \cdot x + c = 0 $

To solve these, one uses the quadratic formula:
$ x = \frac{-b \pm \sqrt{b^{2} - 4ac}}{2a} $

There is a problem, though: if $b^2-4ac$ is less than zero, then it will fail. Write a program that can calculate x for a quadratic equation. Create a function that prints out the roots of a quadratic equation, given a, b, c. When the program detects an equation with no real roots, have it print out a message. How do you know that your results are plausible? Can you check that they are correct?

8. Write a program that reads and stores a series of integers and then computes the sum of the first N integers. First ask for N, then read the values into a vector, then calculate the sum of the first N values. For example:

"Please enter the number of values you want to sum:"

**3**

"Please enter some integers (press 'q' to stop):"

**12 23 13 24 15** |

"The sum of the first **3** numbers (**12 23 13**) is **48**."

Handle all inputs. For example, make sure to give an error message if the user asks for a sum of more numbers than there are in the vector.

9. Modify the program from exercise 8 to write out an error if the result cannot be represented as an `int`.

10. Modify the program from exercise 8 to use **double** instead of `int`. Also, make a **vector** of *doubles* containing the $N$−1 differences between adjacent values and write out that **vector** of differences.

11. Write a program that writes out the first so many values of the Fibonacci series, that is, the series that starts with 1 1 2 3 5 8 13 21 34. The next number of the series is the sum of the two previous ones. Find the largest Fibonacci number that fits in an `int`.

12. Implement a little guessing game called (for some obscure reason) “Bulls and Cows.” The program has a **vector** of four different integers in the range 0 to 9 (e.g., 1234 but not 1122) and it is the user’s task to discover those numbers by repeated guesses. Say the number to be guessed is 1234 and the user guesses 1359; the response should be “1 bull and 1 cow” because the user got one digit (1) right and in the right position (a bull) and one digit (3) right but in the wrong position (a cow). The guessing continues until the user gets four bulls, that is, has the four digits correct and in the correct order.

13. The program is a bit tedious because the answer is hard-coded into the program. Make a version where the user can play repeatedly (without stopping and restarting the program) and each game has a new set of four digits. You can get four random digits by calling the random number generator `randint(10)` from `std_lib_facilities.h` four times. You will note that if you run that program repeatedly, it will pick the same sequence of four digits each time you start the program. To avoid that, ask the user to enter a number (any number) and call `seed_randint(n)`, also from `std_lib_facilities.h`, where **n** is the number the user entered before calling `randint(10)`. Such an **n** is called a *seed*, and different seeds give different sequences of random numbers.

14. Read (day-of-the-week,value) pairs from standard input. For example:

**Tuesday 23 Friday 56 Tuesday −3 Thursday 99**

Collect all the values for each day of the week in a `vector<int>`. Write out the values of the seven day-of-the-week **vectors**. Print out the sum of the values in each **vector**. Ignore illegal days of the week, such as **Funday**, but accept common synonyms such as **Mon** and **monday**. Write out the number of rejected values.

## Postscript

Do you think we overemphasize errors? As novice programmers we would have thought so. The obvious and natural reaction is “It simply can’t be that bad!” Well, it is that bad. Many of the world’s best brains have been astounded and confounded by the difficulty of writing correct programs. In our experience, good mathematicians are the people most likely to underestimate the problem of bugs, but we all quickly exceed our natural capacity for writing programs that are correct the first time. You have been warned! Fortunately, after 50 years or so, we have a lot of experience in organizing code to minimize problems, and techniques to find the bugs that we – despite our best efforts – inevitably leave in our programs as we first write them. The techniques and examples in this chapter are a good start.

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_204_0.png)

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_205_0.png)

# 6 Writing a Program

> “Programming is understanding.”
>
> – Kristen Nygaard

Writing a program involves gradually refining your ideas of what you want to do and how you want to express it. In this chapter and the next, we will develop a program from a first vague idea through stages of analysis, design, implementation, testing, redesign, and re-implementation. Our aim is to give you some idea of the kind of thinking that goes on when you develop a piece of code. In the process, we discuss program organization, user-defined types, and input processing.

## 6.1 A problem

Writing a program starts with a problem; that is, you have a problem that you’d like a program to help solve. Understanding that problem is key to a good program. After all, a program that solves the wrong problem is likely to be of little use to you, however elegant it may be. There are happy accidents when a program just happens to be useful for something for which it was never intended, but let’s not rely on such rare luck. What we want is a program that simply and cleanly solves the problem we decided to solve.

At this stage, what would be a good program to look at? A program that

- Illustrates design and programming techniques
- Gives us a chance to explore the kinds of decisions that a programmer must make and the considerations that go into such decisions
- Doesn’t require too many new programming language constructs
- Is complicated enough to require thought about its design
- Allows for many variations in its solution
- Solves an easily understood problem
- Solves a problem that’s worth solving
- Has a solution that is small enough to completely present and completely comprehend

We chose “Get the computer to do ordinary arithmetic on expressions we type in”; that is, we want to write a simple calculator. Such programs are clearly useful; every desktop computer comes with such a program, and you can even buy computers specially built to run nothing but such programs: pocket calculators.
