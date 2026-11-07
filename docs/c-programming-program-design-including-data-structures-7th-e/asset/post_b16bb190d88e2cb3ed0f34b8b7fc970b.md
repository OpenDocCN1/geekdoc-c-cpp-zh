
```cpp
case 5:
case 7:
    cout << "Odd";
    break;
}
```

27. Suppose that score is an int variable. Consider the following C++ code: (3, 11)

```cpp
int score;
cin >> score;
switch (score % 7)
{
case 0:
    score = score / 2 - 1;
    break;
case 1: case 3:
    score = 3 * score + 1;
    break;
case 2:
    ++score;
    break;
case 4:
    break;
case 5: case 6:
    score = score % 3;
    break;
default:
    score = score / 2;
}
cout << score << endl;
```

- a. What is the output if the input is 12?
- b. What is the output if the input is 4?
- c. What is the output if the input is 3?
- d. What is the output if the input is 25?

28. Suppose that beta is an int variable. Consider the following C++ code: (11)

```cpp
cin >> beta;
switch (beta % 8)
{
case 0:
case 1:
    beta = beta + beta;
    break;
case 2:
    beta--;
    break;
case 3:
case 7:
    beta = static_cast<int>(sqrt(beta * 1.0));
    beta = beta / 3;
    break;
case 4:
    beta = beta * beta;
case 5:
case 6:
    beta = 11 - beta;
    break;
default:
    beta = -5;
}

cout << beta << endl;
```

![](img/d0be7fc6d804b63484835c6c8bc67a07_301_0.png)

- a. What is the output if the input is 3?
- b. What is the output if the input is 12?
- c. What is the output if the input is 15?
- d. What is the output if the input is 28?

**29.** Suppose that num is an `int` variable. Consider the following C++ code: (3, 11)

```cpp
cin >> num;
if (num >= 0)
{
    switch (num)
    {
    case 0:
        num = static_cast<int>(pow(num, 3.0));
        break;
    case 2:
        num = ++num;
        break;
    case 4:
        num = num - 4;
        break;
    case 5:
        num = num * 4;
    case 6:
        num = num / 6;
        break;
    case 10:
        num--;
        break;
    default:
        num = -20;
    }
}
else
    num = num + 10;

cout << num << endl;
```

- a. What is the output if the input is 5?
- b. What is the output if the input is 26?
- c. What is the output if the input is 2?
- d. What is the output if the input is −5?

30. In the following code, correct any errors that would prevent the program from compiling or running: (3, 11)

```cpp
include <iostream>

main ()
{
    int num1, num2;
    bool found;

    cout << "Enter two integers: ;
    cin >> num1 >> num2;
    cout << endl;

    if (num1 >= num2) && num2 > 0
        switch (num % num2)
        {
        case 1
            found = (num / num2) >= 6;
            break;
        case 2: case 3
            num1 = num2 / 2;
            break;
        default:
            num2 = num1 * num2;
        }
    else
    {
        found = (2 * num2 < num1);
        if found
            cin >> num2
            num1 = num2 - num1;
            temp = (num1 + num2) / 10;
        if num2
        {
            num1 = num2;
            num2 = temp;
        }

        cout << num1 << " " << num2 << endl;
    }
```

After correcting the code, answer the following questions. (If needed, insert prompt lines to inform the user for the input.)

- a. What is the output if the input is 10 8?
- b. What is the output if the input is 4 9?

31. The following program contains errors. Correct them so that the program will run and output w = 21. (3, 11)

```cpp
#include <iostream>

using namespace std;
```

34. Suppose that billingAmount is a double variable, which denotes the amount you need to pay to the department store. If you pay the full amount, you get $10.00 or 1% of the billingAmount, whichever is smaller, as a credit on your next bill; if you pay at least 50% of the billingAmount, the penalty is 5% of the balance; if you pay at least 20% of the billingAmount and less than 50% of the billingAmount, the penalty is 10% of the balance; otherwise, the penalty is 20% of the balance. Design an algorithm that prompts the user to enter the billing amount and the desired payment. The algorithm then calculates and outputs the credit or the remaining balance. If the amount is not paid in full, the algorithm should also output the penalty amount. (3)

## PROGRAMMING EXERCISES

- 1. Write a program that prompts the user to input a number. The program should then output the number and a message saying whether the number is positive, negative, or zero.

- 2. Write a program that prompts the user to input three numbers. The program should then output the numbers in ascending order.

- 3. Write a program that prompts the user to input an integer between 0 and 35. If the number is less than or equal to 9, the program should output the number; otherwise, it should output A for 10, B for 11, C for 12 . . . and Z for 35. (Hint: Use the cast operator, static_cast<char>(), for numbers >= 10.)

- 4. The statements in the following program are in incorrect order. Rearrange the statements so that they prompt the user to input the shape type (rectangle, circle, or cylinder) and the appropriate dimension of the shape. The program then outputs the following information about the shape: For a rectangle, it outputs the area and perimeter; for a circle, it outputs the area and circumference; and for a cylinder, it outputs the volume and surface area. After rearranging the statements, your program should be properly indented.

```cpp
using namespace std;

#include <iostream>

int main()
{
    string shape;
    double height;

    #include <string>

    cout << "Enter the shape type: (rectangle, circle, cylinder) ";
    cin >> shape;
    cout << endl;
if (shape == "rectangle")
{
    cout << "Area of the circle = "
         << PI * pow(radius, 2.0) << endl;

    cout << "Circumference of the circle: "
         << 2 * PI * radius << endl;

    cout << "Enter the height of the cylinder: ";
    cin >> height;
    cout << endl;

    cout << "Enter the width of the rectangle: ";
    cin >> width;
    cout << endl;

    cout << "Perimeter of the rectangle = "
         << 2 * (length + width) << endl;
    double width;
}
cout << "Surface area of the cylinder: "
     << 2 * PI * radius * height + 2 * PI * pow(radius, 2.0)
     << endl;
}
else if (shape == "circle")
{
    cout << "Enter the radius of the circle: ";
    cin >> radius;
    cout << endl;

    cout << "Volume of the cylinder = "
         << PI * pow(radius, 2.0) * height << endl;
    double length;
}
return 0;
else if (shape == "cylinder")
{
    double radius;

    cout << "Enter the length of the rectangle: ";
    cin >> length;
    cout << endl;

    #include <iomanip>

    cout << "Enter the radius of the base of the cylinder: ";
    cin >> radius;
    cout << endl;
}
const double PI = 3.1416;
cout << "Area of the rectangle = "
     << length * width << endl;
else
     cout << "The program does not handle " << shape << endl;
     cout << fixed << showpoint << setprecision(2);
#include <cmath>
}
```

- 5. In a right triangle, the square of the length of one side is equal to the sum of the squares of the lengths of the other two sides. Write a program that prompts the user to enter the lengths of three sides of a triangle and then outputs a message indicating whether the triangle is a right triangle.

- 6. A box of cookies can hold 24 cookies, and a container can hold 75 boxes of cookies. Write a program that prompts the user to enter the total number of cookies, the number of cookies in a box, and the number of cookie boxes in a container. The program then outputs the number of boxes and the number of containers to ship the cookies. Note that each box must contain the specified number of cookies, and each container must contain the specified number of boxes. If the last box of cookies contains less than the number of specified cookies, you can discard it and output the number of leftover cookies. Similarly, if the last container contains less than the number of specified boxes, you can discard it and output the number of leftover boxes.

- 7. The roots of the quadratic equation $ax^2 + bx + c = 0$, $a \ne 0$ are given by the following formula:

$$\frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$$

In this formula, the term $b^2 - 4ac$ is called the **discriminant**. If $b^2 - 4ac = 0$, then the equation has a single (repeated) root. If $b^2 - 4ac > 0$, the equation has two real roots. If $b^2 - 4ac < 0$, the equation has two complex roots. Write a program that prompts the user to input the value of $a$ (the coefficient of $x^2$), $b$ (the coefficient of $x$), and $c$ (the constant term) and outputs the type of roots of the equation. Furthermore, if $b^2 - 4ac \ge 0$, the program should output the roots of the quadratic equation. *(Hint: Use the function pow from the header file cmath to calculate the square root. Chapter 3 explains how the function pow is used.)*
