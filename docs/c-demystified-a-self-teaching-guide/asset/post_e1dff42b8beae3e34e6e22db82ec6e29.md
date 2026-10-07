
A common programming mistake in a while condition using a logical operator is to use && when you should use || or vice versa. While the logical && operator may seem the obvious choice in this example, the correct choice in other situations may be less intuitive. If you want to loop until a number is not between 1 and 10, the loop would be while (num < 1 || num > 10)? The answer is the latter: the condition always would be false using the && operator since a number cannot be less than 1 and greater than 10. If you wanted to use the condition instead it would be while (num > 1 && num < 10).

Note

The first condition is if num <= 0. If this expression is false, the data is valid, so the issue of whether the user wants to quit does not arise. Accordingly, the second condition, quit is true, is not even evaluated. As discussed in Chapter 7, with a logical && operator, the expression is evaluated only if the rest is true. Therefore, the loop ends with the value of quit being true, its initialized value, and code execution continues with the if / else statement following the loop.

However, if num <= 0 is true, then the data is invalid, and the second condition, quit is true, is evaluated.

The value of quit may be true either to enter data or under two possibilities. The first possibility is that this is the user's first attempt to enter data and the data was invalid. In this case, the user has not yet been asked whether they want to quit. It is assumed they don't have the opportunity to answer when they want to retry. Therefore, the quit variable is initialized to the value of false when it is declared.

The second possibility is that this is the user's later attempt to enter data and the data was invalid. In this case, the user has already been asked whether they want to quit, so the value of quit is based on the user's answer.

If the value of quit is false, the loop continues. If the user wants to quit, then the expression quit == false will be false because the value of quit is true. Therefore, the loop ends with the value of quit being true, and code execution continues with the if / else statement following the loop.

At some point (hopefully) the loop will end, either because the user has entered a valid number or has decided to quit. Conversely, the value of quit being false indicates that the user entered valid data. Accordingly, we use the value of quit in the if / else statement after the loop ends to indicate whether the user wants to try again.

## While (true)

In Chapter 7 we discussed the use of the for loop with the omission of the condition, like for (;). An infinite loop was avoided by using the break keyword inside. Similarly, programmers sometimes make the condition of the while loop always true, like while (true); you may encounter it this way. Here is an example of a modification of the program that asks the user to enter a positive number:

```cpp
#include <iostream>
using namespace std;
int main(void) {
    int num;
    char choice;
    bool quit = false;
    while (true) {
        cout << "Enter a positive number: ";
        cin >> num;
        if (num > 0)
            break;
        else {
            cout << "Number must be positive; try again (Y/N): ";
            cin >> choice;
            if (choice != 'Y') {
                quit = true;
                break;
            }
        }
    }
    if (quit == false) {
        cout << "The number you entered is " << num;
    } else {
        cout << "You did not enter a positive number";
    }
    return 0;
}
```

The advantage of this modification is that it renders unnecessary to prompt the user before the loop. However, the use of while (true) syntax has the disadvantage that the condition that stops the loop cannot be discerned from the parentheses. The do while loop (explained later in this chapter) avoids this disadvantage and is preferable.

## The continue Keyword

You can use the continue keyword in a while loop just as you can in a for loop. As discussed in Chapter 7, the continue keyword, like the break keyword, is used within the code of an if / else structure. If the continue statement is reached, the current iteration of the loop ends, and the next iteration of the loop begins.

Note The % (modulus) operator is used if the remainder is 0, or a multiple of items. While this use of the continue keyword works certainly, as I cautioned in Chapter 7, you should use it (as well as the break keyword) sparsely. Each iteration of a for loop has one end point. However, when you use a continue statement, each iteration has multiple points. This makes your code more difficult to understand and can result in logic errors.

I suggested in Chapter 7 in an example using the for loop that you could use the logical ! operator as an alternative to the continue keyword. Note You could also use the relational != (not equal) operator, changing the if statement to while (counter % 3 != 0).

## Nesting While Loops

In Chapter 7 I showed how you can nest one loop inside another. Similarly, you can nest one loop inside another. You can also nest a while loop inside a loop, or a for loop inside a while loop.

Chapter 7 demonstrated nested loops with a program that prints 5 rows of 10 characters. The following is a modification of that program using nested loops:

```cpp
#include <iostream>
using namespace std;
int main(void) {
    int x = 0;
    while (x++ < 5) {
        int y = 0;
        while (y++ < 5)
            cout << "X";
    }
    return 0;
}
```

The variable y, used as a counter in the inner loop, needs to be reinitialized in the outer loop. The variable y could be declared outside the loops, but it needs to be assigned (reassigned) the value of zero inside the outer loop since the inner loop goes through all of its iterations for each iteration of the outer loop.

Since each loop has a predictable number of iterations, using nested for loops is somewhat simpler than using nested loops. However, both work.

![](img/59a3417a6d5906fae6d8000d4c2cff76_151_0.png)

 The Do While Loop

The do while loop is similar to the while loop. The primary difference is that with a do while loop the condition is tested at the bottom, unlike a while loop where the condition is tested at the top. This means that a do while loop will always execute at least once, whereas a while loop may never execute if all its condition is false at the outset.

## Syntax

The syntax of a do while loop is

```cpp
do {
    statement(s);
} while (condition);
```

The do keyword starts the loop. The statement or statements belonging to the loop are enclosed in curly braces. After the close curly brace, the keyword appears, followed by the condition in parentheses, terminated by a semicolon.

## A Do While Loop Example

The following program is a modification of the one earlier in this chapter that used a while loop to continue to prompt the user a positive number until either the user did or quit, and then output the positive number or the message that the user did not enter a positive number. This modification uses a do loop instead of a while loop:

```cpp
#include <iostream>
using namespace std;
int main(void) {
    int num;
    char choice;
    bool quit = false;
    do {
        cout << "Enter a positive number: ";
        cin >> num;
        if (num <= 0) {
            cout << "Number must be positive; try again (Y/N) : ";
            cin >> choice;
            if (choice != 'Y')
                quit = true;
        }
    } while (num <= 0 && quit == false);
    if (quit) {
        cout << "The number you entered is " << num << " ";
    } else {
        cout << "You did not enter a positive number";
        return 0;
    }
}
```

The following are sample inputs and outputs. The first one has the user successfully enter a positive number first time.
