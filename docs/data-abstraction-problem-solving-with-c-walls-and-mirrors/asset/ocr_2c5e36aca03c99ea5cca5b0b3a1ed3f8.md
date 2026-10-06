# 730 APPENDIX B Important Themes in Programming

Named constants make a program easier to modify

# B.3.1 Named Constants

The use of constants is a way to enhance the modifiability of a program. For example, the restriction that an array must have a predefined, fixed size causes a bit of difficulty. Suppose that a program uses an array to process the tests of the computer science majors at your university. When the program was written, there were 202 computer science majors, so the array was declared by

```
int scores[202];
```

The program processes the array in several ways. For example, it reads the scores, writes the scores, and averages the scores. The pseudocode for each of these tasks can construct such as

```
for (index = 0 through 201)
    Process the score
```

If the number of majors should change, not only do you need to revise the declaration of scores, but also must change each loop that processes the array to reflect the new array size. In addition, other statements in the program might depend on the size of the array. A 202, here—which one to change? On the other hand, if you use a named constant as

```
const int NUMBER_OF_MAJORS = 202;
```

you can declare the array by using

```
int scores[NUMBER_OF_MAJORS];
```

and write the pseudocode for the processing loops in this form:

```
for (index = 0 through NUMBER_OF_MAJORS - 1)
    Process the score
```

If you write variables that depend on the size of the array in terms of the constant NUMBER_OF_MAJORS (such as NUMBER_OF_MAJORS - 1), you can change the array size simply by changing the definition of the constant and compiling the program again.

# B.3.2 The typedef Statement

typedef statements make a program easier to modify

Suppose that your program performs floating-point computations of float variable, but you discover that you need greater precision than float variables. To change the relevant declarations to long double, you would have to locate all such declarations and decide whether to make the change.

You can simplify this by using a typedef statement, which gives another name to an existing data type. For example,

```
typedef float RealType;
```

declares RealType as a synonym for float and allows you to use RealType and float interchangeably. If you declare all the relevant items in the previous program as RealType instead of float, you can make your program easier to modify and read. To revise the precision of computations, you would simply change the typedef statement to

```
typedef long double RealType;
```

# B.4 Ease of Use

Prompt the user for input

Another area where you need to keep people in mind is the design of the user interface. Humans often process a program’s input and output. Here are a few obvious points: