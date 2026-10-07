
## 274 Chapter 6 Branching Statements and Logical Operators

Here is a sample run of the program in Listing 6.9:

```
Enter two integers: 25 28
The larger of 25 and 28 is 28
```

The key part of the program is this statement:

```
int c = a > b ? a : b;
```

It produces the same result as the following statements:

```
int c;
if (a > b)
    c = a;
else
    c = b;
```

Compared to the if else sequence, the conditional operator is more concise but, at first glance, less obvious. One difference between the two approaches is that the conditional operator produces an expression and hence a single value that can be assigned or incorporated into a larger expression, as the program in Listing 6.9 does when it assigns the value of the conditional expression to the variable c. The conditional operator's concise form, unusual syntax, and overall weird appearance make it great favorite among programmers who appreciate those qualities. One trick for the reprehensible goal of concealing the purpose of code is to nest expressions within one another, as the following example shows:

```
for (int i = 0; i < 3; i++)
cout << ((i < 2) ? x[i] : y : x[1]);
```

This is merely an obscure (but, by no means maximally obscure) to print the three strings in the order:
Jason Quillstone at your service

In terms of readability, the conditional operator is best suited for simple relationships and simple expression values:
x = (x > y) ? x : y;

If the code becomes more involved, it can probably be expressed more clearly as an if else statement.

## The switch Statement

Suppose you create a switch menu that allows the user to select one of five choices—for example, Cheap, Moderate, Expensive, Extravagant, and Excessive. You can extend an if else else sequence to handle five alternatives, but the C++ switch statement is easily selecting a choice from an extended list. Here's the general form for a switch statement:

```
switch (integer-expression)
{
    case label1 : statement(s)
    case label2 : statement(s)
    ...
    default : statement(s)
}
```

A C++ switch statement acts as a routing device that tells the computer which line of to execute next. On reaching a switch statement, a program jumps to the line labeled with the value corresponding to the value of integer-expression. For example, if integer-expression has the value 4, the program goes to the line that has a case 4: label. The value integer-expression, as the name suggests, must be an expression that reduces to an integer value. Also each label must be an integer constant. Most often, labels are simple or char constants, such as 1 or 'q', or enumerators. If integer-expression doesn't match any of the labels, the program jumps to the line abled. The default label is optional. If you omit it and there is no match, the program jumps to the next statement following the switch (see Figure 6.3).

The switch statement is different from similar statements in languages as Pascal as a very important way. Each C++ case label functions only as a label, not as a bound-between choices. That is, if a program jumps to a particular line in a switch, it then sequentially executes all the statements following that line in the switch unless explicitly direct otherwise. Execution does not automatically stop at the next case. To make execution stop at the end of a particular group of statements, you must use the break statement. This causes execution to jump to the statement following the switch.

Listing 6.10 shows how to use switch and break together to implement a simple menu for executives. The program uses a showmenu() function to display a set of choices. A switch statement then selects an action based on the user's request.

```
if num is 5          switch (num)
                    {
                               case 1 : statement1
                             break;
                             case 2 : statement2
                             break;
                             case 3 : statement3
                             break;
                             default : statement4
                    program jumps to here
program jumps to here
```

Figure 6.3  The structure of switch statements.

## 276 Chapter 6 Branching Statements and Logical Operators

> Note
> Some hardware/operating system combinations treat the \a escape sequence (used in case 1 in Listing 6.10) as silent.

Listing 6.10 switch.cpp

```cpp
// switch.cpp -- using the switch statement
#include <iostream>
using namespace std;
void showmenu();    // function prototypes
void report();
void comfort();
int main() {
    showmenu();
    int choice;
    cin >> choice;
    while (choice != 5) {
        switch(choice) {
            case 1 : cout << "*a\n";
                break;
            case 2 : report();
                break;
            case 3 : cout << "*The boss was in all day.\n";
                break;
            case 4 : comfort();
                break;
            default : cout << "That's not a choice.\n";
        }
    }
    showmenu();
    cin >> choice;
    cout << "Bye!\n";
    return 0;
}

void showmenu() {
    cout << "Please enter 1, 2, 3, 4, or 5:\n"
        "1) report\n"
        "3) alibi\n"
        "4) comfort\n"
        "5) quit\n";
}
void report() {
cout << "It's been an excellent week for business.\n"
      "Sales are up 120% Expenses are down 35%\n";
}

void comfort() {
  cout << "Your employees think you are the finest CEO\n"
      "in the industry. The board of directors think\n"
      "you are the finest CEO in the industry.\n";
}
```

Here is a sample run of the executive menu program in Listing 6.10:

Please enter 1, 2, 3, 4, or 5:

+   1) alarm
2) report
3) alibi
4) comfort
5) quit

Your employees think you are the finest CEO
in the industry. The board of directors think
you are the finest CEO in the industry.

Please enter 1, 2, 3, 4, or 5:

+   1) alarm
2) report
3) alibi
4) comfort
5) quit

It's been an excellent week for business.
Sales are up 120% Expenses are down 35%.

Please enter 1, 2, 3, 4, or 5:

+   1) alarm
2) report
3) alibi
4) comfort
5) quit

That's not a choice.

Please enter 1, 2, 3, 4, or 5:

+   1) alarm
2) report
3) alibi
4) comfort
5) quit

Bye!

The loop terminates when the user enters 5. Entering 1 through 4 activates the corresponding choice from the switch, and entering 6 triggers the default. Note that input has to be an integer for the program to work correctly. If, for example, you enter a letter, the input statement will fail, and the loop will cycle until you kill the program. To deal with those who do not follow, it's better to use character input.

## Chapter 6 Branching Statements and Logical Operators

To see this how it works. You'll find, for example, that entering 2 causes the program to execute all the statements associated with case 2, 3, 4, and the default. C++ works this way because sort of behavior can be useful. For one thing, it makes it possible to use multiple labels. For example, suppose you rewrite Listing 6.10 using characters instead of integers as menu choices and switch labels. In case, you could use both an uppercase and lowercase label for the same statements: Because there is no break immediately following case 'a',program execution passes on to the next line, which is the statement following case 'A'.

```
char choice;
cin >> choice;
while (choice != 'Q' && choice != 'q')
{
    switch (choice)
    {
        case 'a':
        case 'A': cout << "\a\n"
            break;
        case 'r':
        case 'R': report();
            break;
        case 'l':
        case 'L': cout << "The boss was in all day.\n"
            break;
        case 'c':
        case 'C': comfort();
            break;
        default : cout << "That's not a choice.\n";
    }
    showmenu();
cin >> choice;
}
```

## Using Enumerators as Labels

Listing 6.11 illustrates using enum to define a set of related constants and then using the constants in a switch statement. In general, cin doesn't recognize enumerated types (it can't know how you will define them), so the program reads the choice as an int. When the switch statement compares the int value to an enumerator case label, it promotes the enumerator to int. Also the enumerators are promoted to type int in the while loop test condition.
