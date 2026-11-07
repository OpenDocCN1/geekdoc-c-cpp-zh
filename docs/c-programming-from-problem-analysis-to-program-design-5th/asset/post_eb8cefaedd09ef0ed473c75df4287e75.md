
- 16. Putting a semicolon at the end of the `for` loop (before the body of the `for` loop) is a semantic error. In this case, the action of the `for` loop is empty.

- 17. The syntax of the `do...while` statement is:

```cpp
do
    statement
while (expression);
```

`statement` is called the body of the `do...while` loop.

- 18. Both `while` and `for` loops are called pretest loops. A `do...while` loop is called a posttest loop.

- 19. The `while` and `for` loops may not execute at all, but the `do...while` loop always executes at least once.

- 20. Executing a `break` statement in the body of a loop immediately terminates the loop.

- 21. Executing a `continue` statement in the body of a loop skips the loop’s remaining statements and proceeds with the next iteration.

- 22. When a `continue` statement executes in a `while` or `do...while` loop, the expression update statement in the body of the loop may not execute.

- 23. After a `continue` statement executes in a `for` loop, the update statement is the next statement executed.

## EXERCISES

- 1. Mark the following statements as true or false.

  - a. In a counter-controlled `while` loop, it is not necessary to initialize the loop control variable.
  - b. It is possible that the body of a `while` loop may not execute at all.
  - c. In an infinite `while` loop, the `while` expression (the decision maker) is initially false, but after the first iteration it is always true.
  - d. The `while` loop:

```cpp
j = 0;
while (j <= 10)
    j++;
```

terminates if `j > 10`.

  - e. A sentinel-controlled `while` loop is an event-controlled `while` loop whose termination depends on a special value.
  - f. A loop is a control structure that causes certain statements to execute over and over.
  - g. To read data from a file of an unspecified length, an EOF-controlled loop is a good choice.

![](img/1fbe55537254baeb2b5b7dbaf64956ae_341_0.png)

2. What is the output of the following C++ code?

```cpp
int count = 1;
int y = 100;
while (count < 100)
{
    y = y - 1;
    count++;
}
cout << " y = " << y << " and count = " << count << endl;
```

3. What is the output of the following C++ code?

```cpp
int num = 5;
while (num > 5)
    num = num + 2;
cout << num << endl;
```

4. What is the output of the following C++ code?

```cpp
int num = 1;
while (num < 10)
{
    cout << num << " ";
    num = num + 2;
}
cout << endl;
```

5. When does the following `while` loop terminate?

```cpp
ch = 'D';
while ('A' <= ch && ch <= 'Z')
    ch = static_cast<char>(static_cast<int>(ch) + 1);
```

6. Suppose that the input is 38  35  71  14  -1. What is the output of the following code? Assume all variables are properly declared.

```cpp
cin >> sum;
cin >> num;

for (j = 1; j <= 3; j++)
{
    cin >> num;
    sum = sum + num;
}
cout << "Sum = " << sum << endl;
```

7. Suppose that the input is 38  35  71  14  -1. What is the output of the following code? Assume all variables are properly declared.

```cpp
cin >> sum;
cin >> num;

while (num != -1)
{
    sum = sum + num;
    cin >> num;
}
cout << "Sum = " << sum << endl;
```

8. Suppose that the input is `38 35 71 14 -1`. What is the output of the following code? Assume all variables are properly declared.

```cpp
cin >> num;
sum = num;

while (num != -1)
{
    cin >> num;
    sum = sum + num;
}
cout << "Sum = " << sum << endl;
```

9. Suppose that the input is `38 35 71 14 -1`. What is the output of the following code? Assume all variables are properly declared.

```cpp
sum = 0;
cin >> num;

while (num != -1)
{
    sum = sum + num;
    cin >> num;
}
cout << "Sum = " << sum << endl;
```

10. Correct the following code so that it finds the sum of 20 numbers.

```cpp
sum = 0;

while (count < 20)
    cin >> num;
    sum = sum + num;
    count++;
```

11. What is the output of the following program?

```cpp
#include <iostream>

using namespace std;

int main()
{
    int x, y, z;

    x = 4;  y = 5;
    z = y + 6;

    while ((z - x) % 4 != 0)
    {
        cout << z << " ";
        z = z + 7;
    }
}
```

```cpp
cout << fixed << showpoint << setprecision(2);

while (response == 'Y' || response == 'y')
{
    cout << "Enter two numbers: ";
    cin >> num1 >> num2;
    cout << endl;

    cout << num1 << " + " << num2 << " = " << (num1 + num2)
         << endl;

    cout << "Would you like to add again: (Y/y) ";
    cin >> response;
    cout << endl;
}

return 0;
}
```

14. What is the output of the following program segment?

```cpp
int count = 0;

while (count++ < 10)
    cout << "This loop can repeat statements." << endl;
```

15. What is the output of the following program segment?

```cpp
int count = 5;

while (--count > 0)
    cout << count << " ";
cout << endl;
```

16. What is the output of the following program segment?

```cpp
int count = 5;

while (count-- > 0)
    cout << count << " ";
cout << endl;
```

17. What is the output of the following program segment?

```cpp
int count = 1;
while (count++ <= 5)
    cout << count * (count - 2) << " ";

cout << endl;
```

18. What type of loop, such as counter-control and sentinel-control, will you use in each of the following situations?

  - a. Sum the following series: 1 + (2 / 1) + (3 / 2) + (4 / 3) + (5 / 4) + ... + (10 / 9)
  - b. Sum the following numbers, except the last number: 17, 32, 62, 48, 58, -1
  - c. A file contains an employee’s salary. Update the employee’s salary.

19. Consider the following for loop:

```cpp
int j, s;

s = 0;
for (j = 1; j <= 10; j++)
    s = s + j * (j - 1);
```

In this for loop, identify the loop control variable, the initialization statement, the loop condition, the update statement, and the statement that updates the value of s.

20. Given that the following code is correctly inserted into a program, state its entire output as to content and form. (Assume all variables are properly declared.)

```cpp
num = 0;
for (i = 1; i <= 4; i++)
{
    num = num + 10 * (i - 1);
    cout << num << " ";
}
cout << endl;
```

21. Given that the following code is correctly inserted into a program, state its entire output as to content and form. (Assume all variables are properly declared.)

```cpp
j = 2;
for (i = 0; i <= 5; i++)
{
    cout << j << " ";
    j = 2 * j + 3;
}
cout << j << " " << endl;
```

22. Assume that the following code is correctly inserted into a program:

```cpp
int s = 0;

for (i = 0; i < 5; i++)
{
    s = 2 * s + i;
    cout << s << " ";
}
cout << endl;
```

  - a. What is the final value of s?
    - (i) 11
    - (ii) 4
    - (iii) 26
    - (iv) none of these
  - b. If a semicolon is inserted after the right parenthesis in the for loop statement, what is the final value of s?
    - (i) 0
    - (ii) 1
    - (iii) 2
    - (iv) 5
    - (v) none of these
  - c. If the 5 is replaced with a 0 in the for loop control expression, what is the final value of s?
    - (i) 0
    - (ii) 1
    - (iii) 2
    - (iv) none of these

```cpp
for (j = 0; j < 8; j++)
{
    cout << j * 25 << " - ";

    if (j != 7)
        cout << (j + 1) * 25 - 1 << endl;
    else
        cout << (j + 1) * 25 << endl;
}
```

28. Suppose that the input is 38  35  71  44  -1. What is the output of the following code? Assume all variables are properly declared.

```cpp
sum = 0;
cin >> num;

for (j = 1; j <= 3; j++)
{
    cin >> num;
    sum = sum + num;
}
cout << "Sum = " << sum << endl;
```

29. Which of the following apply to the **while** loop only? To the **do...while** loop only? To both?

  - a. It is considered a conditional loop.
  - b. The body of the loop executes at least once.
  - c. The logical expression controlling the loop is evaluated before the loop is entered.
  - d. The body of the loop may not execute at all.

30. The following program has more than five mistakes that prevent it from compiling and/or running. Correct all such mistakes.

```cpp
#include <iostream>

using namespace std;
const int N = 2,137;

main ()
{
    int a, b, c, d;

    a = 3;
    b = 5;
    c = c + d;
    N = a + n;
    for (i = 3; i <= N; i++)
    {
        cout << setw(5) << i;
        i = i + 1;
    }
    return 0;
}
```
