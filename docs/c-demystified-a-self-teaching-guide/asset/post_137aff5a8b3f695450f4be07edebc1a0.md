
precedence. Thus, the multiplication operator and the two division operators have equal precedence. Similarly, the addition and subtraction operators have equal precedence.

Table 4-4 shows the results of applying precedence to several arithmetic expressions. We have not reviewed the division operators, yet in the examples in Table 4-4 the / operator works exactly as it does in arithmetic.

## Table 4-4: Precedence in Action

| Expression | Result |
|---|---|
| 2 + 3 * 4 | 14, not 20 |
| 8 / 2 - 1 | 3, not 8 |

C++ also has rules associativity for determining which operation is performed first when two operators have equal precedence. Table 4-5 describes these rules.

## Table 4-5: Associativity of Arithmetic Operators

| Operator | Associativity |
|---|---|
| (unary negation) | Left to right |
| * / % | Left to right |
| - | Left to right |

Therefore, the result of the expression 8 / 2 * 4 is 16, not 1, because division, the leftmost operator, is performed first.

However, there are times when you need to override the default precedence. For example, in our program, calculating tuition, the default precedence would be multiplied by 72, after which the product would be added to total. However we want to change the order of operations so that dropped is added to total, and the sum multiplied by 72.

You can override the default precedence. This is in the statement:
```cpp
cout << "Total tuition owed: $" << (total + dropped) * 72 << endl;
```

Expressions in parentheses are first. As a result of the parentheses, the expression (total + dropped) * 72 is evaluated so that dropped is first added to total, and the sum is multiplied by 72.

## Division Operators

Addition, subtraction, and multiplication each have one operator. However, division has two. / operator gives you the quotient, the % (or modulus) gives you the remainder.

Quotient and remainder, along dividend and divisor, are terms I first learned in elementary school and did not use much until many years later. If this example may help. In the problem 7 divided by 2, the dividend is 7 and the divisor is 2. The result of this division is 3 and the remainder

## The Division Operator

The division operator returns the quotient. However, the value of the quotient depends on whether at least one of the operands is a floating point data type.

For example, the value of 10 / 4 is 2.5. However, in C++, the value is 2 because, when both operands are an integer or whole number data type, the result is an integer as well, and the remainder is not part of the quotient. This is true even if the result is assigned to a floating point variable. The output of the following program is 10 / 4 = 2.

```cpp
#include <iostream>
using namespace std;
int main(void)
{
    int firstOp = 10, secondOp = 4;
    float result = firstOp / secondOp;
    cout << firstOp << " / " << secondOp << " = " << result;
    return 0;
}
```

However, the value of 10.0 / 4 is 2.5 in C++. When at least one of the operands is a floating point data type, and 10.0 would be interpreted as floating point, then the result is a floating point as well. The output of the following program is 10 / 4 = 2.5 because we changed the data type of firstOp from int to float:

```cpp
#include <iostream>
using namespace std;
int main(void)
{
    float firstOp = 10, result;
    int secondOp = 4;
    result = firstOp / secondOp;
    cout << firstOp << " / " << secondOp << " = " << result;
    return 0;
}
```

Going back to the first example, if you want the division of two integer variables to be a float, then you have to cast one of the variables to the float. A cast does not change the data type of the operation, just the data type of the value during the completion of the operation. You can change the variable by putting the desired data type in front of it in an expression, and placing either the desired type or the variable in parentheses. This is how the first example could be changed to make the result of integer division a float:

```cpp
#include <iostream>
using namespace std;
int main(void)
{
    int firstOp = 10, secondOp = 4;
    float result = (float)firstOp / secondOp;
    cout << firstOp << " / " << secondOp << " = " << result;
    return 0;
}
```

All of the following expressions would work

```cpp
float result = (float)firstOp / secondOp;
float result = firstOp / (float)secondOp;
```

## Arithmetic Operators

```cpp
float result = firstOp / (float) secondOp;
float result = firstOp / float (secondOp);
```

However, in some programs you may want integer division so that the quotient ignore the fractional value. The Change Machine project in the header is an example. In the last

Let's put this into practice with the student enrollment program. In the last modification to this program, tuition was calculated based on all students who were enrolled in the course, even if they no longer were in the course. The addition to the program calculates displays the average tuition per student still enrolled. An integer variable tuition added to store the total tuition collected, which is calculated using the expression (total + dropped) * 72. The average tuition per student still enrolled is calculated and displayed with the statement:

```cpp
cout << "Average tuition per enrolled student: $" << (float)tuition / total;
```

## The code now reads

```cpp
#include <iostream>
#include <string>
using namespace std;
int main(void)
{
    int total, added, dropped, tuition;
    cout << "Enter number of preregistered students: ";
    cin >> total;
    cout << "Enter number of students adding the course: ";
    cin >> added;
    total = total + added;
    cout << "How many students dropped? ";
    cin >> dropped;
    total -= dropped;
    cout << "Total number of students: " << total << endl;
    tuition = (total + dropped) * 72;
    cout << "Total tuition owed: $" << tuition << endl;
    cout << "Average tuition per enrolled student: $" << (float)tuition / total;
    return 0;
}
```

```
Enter number of preregistered students: 30
Enter number of students adding the course: 3
How many students dropped? 5
Total number of students: 28
Total tuition owed: $2376
Average tuition per enrolled student: $84.8571
```

The casting of one of the operands is necessary. Otherwise, the average tuition would be 84 instead of 84.571.

## The Modulus Operator

The modulus operator also involves division, but returns only the remainder. For example, the result of 7 % 2 is not the quotient, but the remainder, 1.

The modulus operator works only with whole number operands. The result of an attempt to use it with a floating point operand is undefined. The result often is a compiler error, but this is compiler dependent.

The modulus operator will be used in Change Machine project later in this chapter.

**Caution** Whether you use the / or % operator, you cannot divide by zero. The result is an error.

## Exponents

C++, unlike some other languages, does not have an exponent operator. Instead, it has a built-in function named pow, which is defined in the standard library cmath. The name pow is shorthand for power, since with exponents one is raised to the power of another.

The pow function has two arguments. The first argument is the number that is being raised to a certain power. The second argument is the power argument being raised to. Therefore, the expression pow(4, 2) is used to raise 4 to the power of 2, the result being 16.

While in the example 4 to the power of 2, the result is a whole number, the pow function returns a double type. Floating point numbers can also be raised to, resulting in another floating point number. Additionally, whole numbers can be raised to a negative power, which may also result in a floating point number.

The pow function is useful for solving math. The formula for the area of a circle is area = π * 3.14159, two double variables area and radius, and that has already been assigned a value, the code for determining the circle's area

area = 3.14159 * pow(radius, 2);

The following program calculates the area of a circle based on a radius inputted by the user.

```cpp
#include <iostream>
#include <cmath>
using namespace std;
int main(void)
{
    double radius, area;
    cout << "Enter radius of circle: ";
    cin >> radius;
    area = 3.14159 * pow(radius, 2);
    cout << "The area is " << area << endl;
    return 0;
}
```

The input and output could be
Enter radius of circle: 6
The area is 113.097
