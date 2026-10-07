# Precedence Between Arithmetic Assignment Operators

The statement total = total + added uses two operators, assignment and arithmetic. The arithmetic operation has precedence over the assignment operation. This means the addition is performed before the assignment. This makes more sense intuitively than the other order. However, as I will explain in detail this chapter, precedence also arises when more than one operator is used in a statement, and there the correct order is less intuitive.

# Overflow and Underflow

Overflow and underflow applies to the results of addition. The range of the int data type on my compiler and operating system is -2,147,483,648 to 2,147,483,647. Here is the result of my starting with a large preregistration,2,147,483,647, and then adding one more student:

+   * Enter number of prereistered students: 2147483647
* Enter number of students adding the course: 1
* Total number of students: -2147483648

While negative inputs make no sense in this program since you can't have a negative number of students enrolled in or add a class, other programs may use negative numbers, for as below zero temperatures. Therefore, the following input uses negative numbers to illustrate underflow with the addition operator.

+   * Enter number of prereistered students: -2147483648
* Enter number of students adding the course: -1
* Total number of students: 2147483647

# Adding Strings

While we think of adding numeric operands, the addition operator can also be used with string operands. The output of the following code is: "Your name is JeffKent."

```
#include <iostream>
#include <string>
using namespace std;
int main(void)
{
    string firstName = "Jeff";
    string lastName = "Kent";
    cout << "Your name is " << firstName + lastName;
    return 0;
}
```

Adding two strings has the effect of appending the second string operand to the first string operand. Adding means adding the content of the second string to the end of the first string.

While you can add numbers and numbers, or strings and strings, attempting to add a number and a string will cause a compiler error. The addition operator may perform arithmetic with two numeric operands, or appending with two string operands, but it does not know how to add a numeric operand and a string operand.

# The Subtraction Operator

At the community college where I teach, students leave the class as join it. Some