
Greatest common divisor of x and y, defined recursively as follows: If y is equal to 0, then gcd(x, y) is x; otherwise, gcd(x, y) is gcd(y, x % y), where % is the modulus operator. [Note: For this algorithm, x must be larger than y.]

### 6.42 (Recursive main)

Can main be called recursively on your system? Write a program containing a function main. Include static local variable count and initialize it to 1. Postincrement and print the value of count each time main is called. Compile your program. What happens?

### 6.43 (Distance Between Points)

Write function distance that calculates the distance between two points (x₁, y₁) and (x₂, y₂). All numbers and return values should be of type double.

### 6.44

What’s wrong with the following program?

```cpp
// Exercise 6.44: ex06_44.cpp
// What is wrong with this program?
#include <iostream>
using namespace std;

int main()
{
    int c;

    if ( ( c = cin.get() ) != EOF )
    {
        main();
        cout << c;
    } // end if
} // end main
```

### 6.45

What does the following program do?

```cpp
// Exercise 6.45: ex06_45.cpp
// What does this program do?
#include <iostream>
using namespace std;

int mystery( int, int ); // function prototype

int main()
{
    int x, y;

    cout << "Enter two integers: ";
    cin >> x >> y;
    cout << "The result is " << mystery( x, y ) << endl;
} // end main

// Parameter b must be a positive integer to prevent infinite recursion
int mystery( int a, int b )
{
    if ( b == 1 ) // base case
        return a;
    else // recursion step
        return a + mystery( a, b - 1 );
} // end function mystery
```

### 6.46

After you determine what the program of Exercise 6.45 does, modify the program to function properly after removing the restriction that the second argument be nonnegative.

### 6.47 (Math Library Functions)

Write a program that tests as many of the math library functions in Fig. 6.2 as you can. Exercise each of these functions by having your program print out tables of return values for a diversity of argument values.

### 6.48 (Find the Error)

Find the error in each of the following program segments and explain how to correct it:

a)
```cpp
float cube( float );  // function prototype

cube( float number )  // function definition
{
    return number * number * number;
}
```

b)
```cpp
register auto int x = 7;
```

c)
```cpp
int randomNumber = srand();
```

d)
```cpp
float y = 123.45678;
int x;

x = y;
cout << static_cast< float >( x ) << endl;
```

e)
```cpp
double square( double number )
{
    double number;
    return number * number;
}
```

f)
```cpp
int sum( int n )
{
    if ( n == 0 )
        return 0;
    else
        return n + sum( n );
}
```

### 6.49 (Craps Game Modification)

Modify the craps program of Fig. 6.11 to allow wagering. Package as a function the portion of the program that runs one game of craps. Initialize variable `bankBalance` to 1000 dollars. Prompt the player to enter a wager. Use a while loop to check that wager is less than or equal to `bankBalance` and, if not, prompt the user to reenter wager until a valid wager is entered. After a correct wager is entered, run one game of craps. If the player wins, increase `bankBalance` by wager and print the new `bankBalance`. If the player loses, decrease `bankBalance` by wager, print the new `bankBalance`, check on whether `bankBalance` has become zero and, if so, print the message "Sorry. You busted!" As the game progresses, print various messages to create some “chatter” such as “Oh, you’re going for broke, huh?” “Aw c’mon, take a chance!” or “You’re up big. Now’s the time to cash in your chips!”.

### 6.50 (Circle Area)

Write a C++ program that prompts the user for the radius of a circle, then calls inline function `circleArea` to calculate the area of that circle.

### 6.51 (Pass-by-Value vs. Pass-by-Reference)

Write a complete C++ program with the two alternate functions specified below, each of which simply triples the variable contained in `main`. Then compare and contrast the two approaches. These two functions are:

- a) function `tripleByValue` that passes a copy of `count` by value, triples the copy and returns the new value and
- b) function `tripleByReference` that passes `count` by reference via a reference parameter and triples the original value of `count` through its alias (i.e., the reference parameter).

### 6.52

What’s the purpose of the unary scope resolution operator?

### 6.53 (Function Template minimum)

Write a program that uses a function template called `minimum` to determine the smaller of two arguments. Test the program using integer, character and floating-point number arguments.

### 6.54 (Function Template maximum)

Write a program that uses a function template called `maximum` to determine the larger of two arguments. Test the program using integer, character and floating-point number arguments.

### 6.55 (Find the Error)

Determine whether the following program segments contain errors. For each error, explain how it can be corrected. [Note: For a particular program segment, it’s possible that no errors are present in the segment.]

a)
```cpp
template < class A >
int sum( int num1, int num2, int num3 )
{
    return num1 + num2 + num3;
}
```

b)
```cpp
void printResults( int x, int y )
{
    cout << "The sum is " << x + y << '\n';
    return x + y;
}
```

c)
```cpp
template < A >
A product( A num1, A num2, A num3 )
{
    return num1 * num2 * num3;
}
```

d)
```cpp
double cube( int );
int cube( int );
```

## Making a Difference

As computer costs decline, it becomes feasible for every student, regardless of economic circumstance, to have a computer and use it in school. This creates exciting possibilities for improving the educational experience of all students worldwide as suggested by the next five exercises. [Note: Check out initiatives such as the One Laptop Per Child Project (www.laptop.org). Also, research “green” laptops—and note the key “going green” characteristics of these devices. Look into the Electronic Product Environmental Assessment Tool (www.epeat.net), which can help you assess the “greenness” of desktops, notebooks and monitors to help you decide which products to purchase.]

### 6.56 (Computer-Assisted Instruction)

The use of computers in education is referred to as *computer-assisted instruction* (*CAI*). Write a program that will help an elementary school student learn multiplication. Use the rand function to produce two positive one-digit integers. The program should then prompt the user with a question, such as

> How much is 6 times 7?

The student then inputs the answer. Next, the program checks the student’s answer. If it’s correct, display the message "Very good!" and ask another multiplication question. If the answer is wrong, display the message "No. Please try again." and let the student try the same question repeatedly until the student finally gets it right. A separate function should be used to generate each new question. This function should be called once when the application begins execution and each time the user answers the question correctly.

### 6.57 (Computer-Assisted Instruction: Reducing Student Fatigue)

One problem in CAI environments is student fatigue. This can be reduced by varying the computer’s responses to hold the student’s attention. Modify the program of Exercise 6.56 so that various comments are displayed for each answer as follows:

- **Possible responses to a correct answer:**
  - Very good!
  - Excellent!
  - Nice work!
  - Keep up the good work!
- **Possible responses to an incorrect answer:**
  - No. Please try again.
  - Wrong. Try one more.
  - Don't give up!
  - No. Keep trying.

Use random-number generation to choose a number from 1 to 4 that will be used to select one of the four appropriate responses to each correct or incorrect answer. Use a switch statement to issue the responses.

### 6.58 (Computer-Assisted Instruction: Monitoring Student Performance)

More sophisticated computer-assisted instruction systems monitor the student’s performance over a period of time. The decision to begin a new topic is often based on the student’s success with previous topics. Modify the program of Exercise 6.57 to count the number of correct and incorrect responses typed by the student. After the student types 10 answers, your program should calculate the percentage that are correct. If the percentage is lower than 75%, display "Please ask your teacher for extra help.", then reset the program so another student can try it. If the percentage is 75% or higher, display "Congratulations, you are ready to go to the next level!", then reset the program so another student can try it.

### 6.59 (Computer-Assisted Instruction: Difficulty Levels)

Exercises 6.56–6.58 developed a computer-assisted instruction program to help teach an elementary school student multiplication. Modify the program to allow the user to enter a difficulty level. At a difficulty level of 1, the program should use only single-digit numbers in the problems; at a difficulty level of 2, numbers as large as two digits, and so on.

### 6.60 (Computer-Assisted Instruction: Varying the Types of Problems)

Modify the program of Exercise 6.59 to allow the user to pick a type of arithmetic problem to study. An option of 1 means addition problems only, 2 means subtraction problems only, 3 means multiplication problems only, 4 means division problems only and 5 means a random mixture of all these types.
