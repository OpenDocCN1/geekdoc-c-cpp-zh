
declares that the variable firstName will store a character string; and the statement

```
cin >> firstName;
```

uses the >> operator to read the character string entered by the user from the keyboard (cin) and stores it in variable firstName. The next statement

```
cout << "\nWelcome to CS 104, " << firstName << "!\n";
```

then displays on the screen a personalized greeting consisting of

+   1. a special character (\n) that causes an advance to a new line followed by the string
+      Welcome to CS 104,
+   2. the character string that is stored in firstName
+   3. the character ! followed by the new-line character

## 2.2 PROGRAMMING AND PROBLEM SOLVING—AN OVERVIEW

A computer program is a sequence of instructions that must be followed to solve some problem, and the main reason that people learn programming is so that they can use the computer as a problem-solving tool. At least four steps or stages can be identified in the program-development process:

+   1. Design: Analyze the problem and design a solution, which results in an algorithm to solve the problem. This is usually the most difficult part of the development process because it basically requires that the programmer knows how to go about solving the problem.
+   2. Coding: Translate the design plan into the syntax of a high-level language such as C++ to produce a program.
+   3. Testing, Execution, and Debugging: Repeatedly test the program, removing errors (called bugs) until one is confident that it solves the problem.
+   4. Maintenance: Over time, the program is updated and modified, as necessary, to meet the changing needs of its users.

In this section these steps are illustrated with an example that is quite simple so that the main ideas are emphasized at each stage without getting lost in a maze of details.

### 2.2.1 Problem: Temperature Conversion

A marine biologist is conducting research on microorganisms in the Great Lakes. One part of this study involves the effect of sudden changes in water temperature. The reading she just recorded was 17.35°C, but some of the formulas she uses to analyze data require

that the temperatures be in Fahrenheit. She would like a program she can use to convert a Celsius temperature to Fahrenheit.

### 2.2.2 Program Design

Problems to be solved are usually expressed in a natural language such as English and often are stated imprecisely, making it necessary to analyze the problem and formulate it more precisely. For the preceding problem, this is quite easy:

Given a temperature reading in Celsius, compute the equivalent Fahrenheit temperature.

For many problems, however, this may be considerably more difficult, because the initial descriptions may be quite vague and imprecise, perhaps because the people who pose the problems do not understand them well nor how to solve them nor what the computer’s capabilities and limitations are.

We will call the approach used in this text to design software solutions to problems object-centered design (OCD) because it focuses on objects that are given in the problem (the input); objects that make up the solution of the problem (the output); and other objects that may be needed to obtain the solution. In its simplest form, it consists of the following stages:

+   1. Behavior: Describe how you want the program to behave.
+   2. Objects: Identify the real-world objects in this description and categorize them.
+   3. Operations: Identify the operations needed to solve the problem.
+   4. Algorithm: Arrange these objects and operations in an order that solves the problem.

#### 2.2.2.1 Behavior

We begin by writing out what we want our program to do (i.e., how we want it to behave). Because the remainder of our design depends on this step, we try to make it as precise as possible:

Behavior: The program should display a prompt for the Celsius temperature on the screen and should then read this Celsius temperature from the keyboard. It should then compute the corresponding Fahrenheit temperature and display it on the screen.

Note that we have generalized the problem to convert an arbitrary Celsius temperature and not just 17.35°C. Such generalization is an important aspect of analyzing a problem because programs should be sufficiently flexible to solve not only the given specific problem, but also any related problem of the same kind with little, if any, modification required.

#### 2.2.2.2 Objects

Once we have decided exactly what the program should do, we are ready for the next step of identifying the objects in the problem. One simple approach is to identify the noun phrases in our behavioral description, ignoring nouns like user and program:

Behavior: The program should display a prompt for the Celsius temperature on the screen and should then read this Celsius temperature from the keyboard. It should then compute the corresponding Fahrenheit temperature and display it on the screen.

This gives us the following list of objects:

+   Problem's Objects:
+   - prompt for the Celsius temperature
+   - screen
+   - Celsius temperature
+   - keyboard
+   - Fahrenheit temperature

They must be represented in a programming language by software objects, which in most programming languages must have a specified type that tells what kind of values they can have. Some of them will have values that vary from one execution of the program to the next and/or during execution; they are called variables and must have names. Those whose values remain constant may or may not be named. In our example, we can classify our objects as follows:

| Problem Objects | Software Objects |  |  |
|---|---|---|---|
|  | Type | Kind | Name |
| prompt for Celsius temperature | text string | constant | none |
| screen | output device | variable | cout |
| Celsius temperature | real number | variable | celsius |
| keyboard | input device | variable | cin |
| Fahrenheit temperature | real number | variable | fahrenheit |

We will not name the first software object in our problem, the prompt, because its value does not change during execution of the program and is unlikely to change in the future. In a C++ program, such text string constants are enclosed within double quotes.

The predefined name cout in C++ refers to the output screen (or window). Because the contents of the screen will change during program execution, it is considered to be a variable.

We have chosen the name celsius for the third software object, the Celsius temperature. Its value will vary from one execution to the next because the user enters that value from the keyboard. Numeric objects that can store real values (i.e., numbers with decimal points) are represented by the type double (or float) in C++.

The predefined name cin in C++ refers to the keyboard. Because values will be entered from it during program execution, it too is considered to be a variable.

Finally, we have chosen the name fahrenheit for our last software object, the Fahrenheit temperature. It is a variable, because its value will be computed using the value of celsius.

#### 2.2.2.3 Operations

Now that we have identified and classified the objects in our program, we can proceed to the next step, which is to identify the operations needed to solve the problem. For the objects we identified the nouns in our behavioral description; for the operations we can begin by identifying the verbs that describe actions of the program:

Behavior: The program should display a prompt for the Celsius temperature on the screen and should then read this Celsius temperature from the keyboard. It should then compute the corresponding Fahrenheit temperature and display it on the screen.

Using the objects we identified earlier, we can describe these operations as follows:

+   Problem's Operations:
+   Output a prompt for the Celsius temperature to cout
+   Input a real value from cin and store it in celsius
+   Compute fahrenheit
+   Output the value of fahrenheit to cout

C++ provides the operator << that we can use to output the prompt for the Celsius temperature and the value of fahrenheit to cout (i.e, the screen). Similarly, we can use C++'s operator >> to input a real value from cin (i.e., the keyboard) and store it in celsius.

Computing the value of fahrenheit requires some additional work. Using the formula

fahrenheit = 1.8 × celsius + 32.0

means that we need to expand our list of operations:

+   Problem's Operations:
+   Output a prompt for the Celsius temperature to cout
+   Input a real value from cin and store it in celsius
+   Compute fahrenheit:
+   Multiply real values: 1.8 and celsius
+   Add real values: the preceding product and 32.0
+   Output the value of fahrenheit to cout

In most languages, including C++, real values can be multiplied using the * operator and can be added using the + operator. Thus, C++ provides all of the operations needed
