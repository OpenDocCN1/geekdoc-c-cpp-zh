
**Table 9: Relational operator**

| Operator | Meaning | Associativity |
|---|---|---|
| == | Equality | Left to right |
| != | Inequality | Left to right |

Listing 18 shows how to check that the value stored in variable budget is greater than 0 or not, using the < relational operator and the if-else statement (you can find the RelationalEx.cpp file on the CD in the code/chapter1 folder):

### ▶ Listing 18: Using the < Relational Operator

```cpp
#include <iostream.h>

int main()
{
    int budget = 1;
    if (budget < 0)
    {
        cout << "budget is less than 0" << endl;
    }
    else
    {
        cout << "budget is greater than 0" << endl;
    }
    return 0;
}
```

Output:

```text
budget is greater than 0
```

In Listing 18, we declare a `budget` variable and initialize it with an integer value 1. Then, we place a conditional `if` statement to check whether the value of the `budget` variable is less than 0 or not. After this, the `budget` is less than 0 value is displayed; however, if the value of the `budget` variable is not less than 0, then the value `budget` is greater than 0 is displayed.

> Most of the time, novice programmers use the assignment operator `=` and relational operator `==` interchangeably. This may result in a logical error and affect the overall output of the program. Therefore, while comparing two values, bear in mind that you must use the `==` (relational) operator instead of the `=` (assignment) operator. For example, the expression `budget = 0` is true, in case the value in the budget variable is 0. On the other hand, the expression `budget == 0` assigns a value of 0 to budget, and the result of that expression is 0, which is false. So, you need to be careful while using the `=` operator in a C++ program.

## TEST YOUR KNOWLEDGE

Q12. Write a program to implement relational operators.

Ans.

```cpp
#include <iostream.h>

int main()
{
    int age = 18;
    if (age >= 18)
    {
        cout << "Eligible to vote " << endl;
    }
    else
    {
        cout << "Not eligible to vote" << endl;
    }
    return 0;
}
```

Output:

```text
Eligible to vote
```

## Logical Operators

The logical operators of C++ are used to combine logical expressions. The two logical operators that are usually used in logical expressions are:

- The && (logical And) operator: Returns true when both operands are true, and false otherwise
- The || (logical Or) operator: Returns false when both operands are false, and true otherwise

These operators tie logical expressions together in a way that matches their names-use, also when you want both logical clauses to be true and/or when you require only one of clauses to be true. These operators work with operands, as shown in Table 10:

| X | Y | x \|\| y (Or) | X && y (AND) |
|---|---|---|---|
| false | false | false | false |
| true | false | true | false |
| false | true | true | false |
| true | true | true | true |

Now, consider Listing 19 in which we have used the && operator. In this case, the value in temperature must be both less than 90 and greater than 60 for the condition within the if-else statement's parentheses to be true. Listing 19 shows the use of the && (AND) operator (you can find the AndOperatorEx.cpp file on the CD in the code/chapter1 folder):

### ▶ Listing 19: Using the && Operator

```cpp
#include <iostream.h>

int main()
{
    int temperature = 70;
    if (temperature < 90 && temperature > 60)
    {
        cout << "Yes! It is a good time for picnic " << endl;
    }
    return 0;
}
```

Output:

Yes! It is a good time for picnic

In Listing 19, we used the && operator in the if expression. Now, let’s understand the use of the || operator. Listing 20 shows the use of the || (OR) operator (you can find the OrOperatorEx.cpp file on the CD in the code/chapter1 folder):

### ▶ Listing 20: Using the || Operator

```cpp
#include <iostream.h>

int main()
{
    int temperature = 50;
    if (temperature > 90 || temperature < 60)
    {
        cout << " Bad weather, no picnic today" << endl;
    }
    else
    {
        cout << "Yes! It is a good time for picnic" << endl;
    }
    return 0;
}
```

Output:

Bad weather, no picnic today

In Listing 20, to evaluate the expressions to true within the `if` statement, the value of the `temperature` variable should be either more than 90 or less than 60. The preceding output shows that the value assigned in the `temperature` variable is less than 60, which lets the expression written within the if statement to be true.

The `&&` and `||` operators are also called short circuit operators, which means that if they can determine all they need to know by evaluating the left operand, they would not evaluate the right operand. This is very useful in cases where we test both, whether or not a value holds 0, and its reciprocal; if the value is indeed 0, the second part of the expression, where its reciprocal is calculated, is not executed; therefore, there is no divide-by-zero overflow error in program.

Listing 21 shows the use of the short circuit operator `&&` (you can find the `ShortEx.cpp` file on the CD in the code/chapter1 folder):

### ▶ Listing 21: Using the Short Circuit Operator

```cpp
#include <iostream>

int main()
{
    double value = 0;
    if (value != 0 && 1/value < 1000)
    {
        cout << "The value is not too small." << endl;
    }
    else
    {
        cout << " The value is too small." << endl;
    }
    return 0;
}
```

Output:

The value is too small.

In Listing 21, to evaluate the expressions to true within the `if` statement, the value of the `value` variable should be not equal to 0, and when you divide 1 with that value the remainder should be less than 1000. The preceding output shows that the value assigned in the `value` variable is 0, which makes the expression written within the `if` statement false. Therefore, the statement written in the `else` block is displayed as the output.

## TEST YOUR KNOWLEDGE

Q13. Write a program to implement logical operators.

Ans.

```cpp
#include <iostream.h>

int main()
{
    int marks = 70;
    if (marks > 50 && marks < 60)
    {
        cout << " B Grade " << endl;
    }
    else
    {
        if (marks > 65 || marks < 75)
        {
            cout << " A Grade " << endl;
        }
    }
    return 0;
}
```

Output:

```text
A Grade
```

> Explain logical operators. Write a C++ program to demonstrate the same (Mumbai University, December 2008)

After understanding the logical operators, let’s now discuss the bitwise operators.

## Bitwise Operators

The operators that allow you to manipulate the individual bits of values are called as bitwise operators. Table 11 lists the bitwise operators supported by C++:

| Operator | Meaning | Associativity |
|---|---|---|
| & | Bitwise AND | Left to right |
| \| | Bitwise OR | Left to right |
| ^ | Bitwise XOR | Left to right |

The & operator compares the corresponding bits of both the operands and if the corresponding bits is 1, then the result is 1 else, the result is 0. In case of the | operator, if any one of the corresponding bits is 1, then the result will be 1 else, it will be 0. The ^ operator compares the corresponding bits and returns 1 when one of the bits is 0 and the other is 1; otherwise, the result is 0.

Listing 22 shows the use of the & (bitwise AND) operator (you can find the BitwiseAndEx.cpp file on the CD in the code/chapter1 folder):

### ▶ Listing 22: Using the Bitwise AND Operator

```cpp
#include <iostream.h>

int main()
{
    int x, y, z;
    x = 15;
    y = 27;
    z = x & y;
    cout<<"The value of operand 1 is: "<<x<<endl;
    cout<<"The value of operand 2 is: "<<y<<endl;
    cout<<"The value of operand 1 and operand 2 is: "<<z<<endl;
    return 0;
}
```

Output:

```text
The value of operand 1 is: 15
The value of operand 2 is: 27
The value of operand 1 and operand 2 is: 11
```

In Listing 22, first, the x, y, and z variables of int type are declared. Next, the x and y variables are assigned the values 15 and 27, respectively. Finally, the bitwise AND operator is used to assign the value to the z variable.

Now, let's discuss the use of the bitwise OR operator. Listing 23 shows how to use the bitwise OR (|) operator (you can find the BitwiseOrEx.cpp file on the CD in the code/chapter1 folder):

### ▶ Listing 23: Using the Bitwise OR Operator

```cpp
#include <iostream.h>

int main()
{
    int x, y, z;
    x = 15;
    y = 27;
    z = x | y;
    cout<<"The value of operand 1 is: "<<x<<endl;
    cout<<"The value of operand 2 is: "<<y<<endl;
    cout<<"The value of operand 1 or operand 2 is: "<<z<<endl;
    return 0;
}
```
