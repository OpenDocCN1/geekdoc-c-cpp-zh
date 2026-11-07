```
    Enter two integers to compare: 22 12
    22 != 12
    22 > 12
    22 >= 12
```

```
    Enter two integers to compare: 7 7
    7 == 7
    7 <= 7
    7 >= 7
```

**Fig. 2.5** | Comparing integers using if statements, relational operators and equality operators. (Part 2 of 2.)

# ### using Declarations

Lines 6–7

```
    using std::cout; // program uses cout
    using std::cin; // program uses cin
```

are using declarations that eliminate the need to repeat the std:: prefix as we did in earlier programs. We can now simply write cout instead of std::cout and cin instead of std::cin in the remainder of the program.

# ### using Directive

In place of lines 6–7, many programmers prefer the using directive

```
    using namespace std;
```

which enables your program to use names from the std namespace without the std:: qualification. In the early chapters, we'll use this directive to simplify the code,² but in Chapter 6 we'll return to using std::, which is considered good practice and can help you avoid some subtle coding errors.

![](bbox=[0.828, 0.608, 0.868, 0.633])

# ### Variable Declarations and Reading the Inputs from the User

Lines 11–12

```
    int number1{0}; // first integer to compare (initialized to 0)
    int number2{0}; // second integer to compare (initialized to 0)
```

declare the variables used in the program and initialize them to 0.

Line 15

```
    cin >> number1 >> number2; // read two integers from user
```

uses cascaded stream extraction operations to input two integers. Recall that we're allowed to write cin (instead of std::cin) because of line 7. This statement first reads a value into number1, then reads another value into number2.

2. In Chapter 20, we'll discuss some disadvantages of using directives in large-scale systems.