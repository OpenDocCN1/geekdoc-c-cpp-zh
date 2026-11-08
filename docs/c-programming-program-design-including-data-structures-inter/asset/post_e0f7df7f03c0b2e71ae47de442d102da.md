
```cpp
while (num != -999)
{
    cout << num % 25 << " ";
    cin >> num;
}

cout << endl;

return 0;
}
```

13. The following program is designed to input two numbers and output their sum. It asks the user if he/she would like to run the program. If the answer is Y or y, it prompts the user to enter two numbers. After adding the numbers and displaying the results, it again asks the user if he/she would like to add more numbers. However, the program fails to do so. Correct the program so that it works properly.

```cpp
#include <iostream>
#include <iomanip>

using namespace std;

int main()
{
    char response;
    double num1;
    double num2;

    cout << "This program adds two numbers." << endl;
    cout << "Would you like to run the program: (Y/y) ";
    cin >> response;
    cout << endl;

    cout << fixed << showpoint << setprecision(2);

    while (response == 'Y' && response == 'y')
    {
        cout << "Enter two numbers: ";
        cin >> num1 >> num2;
        cout << endl;

        cout << num1 << " + " << num2 << " = " << (num1 - num2)
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

- b. Sum the following numbers, except the last number: 17, 32, 62, 48, 58, −1

- c. A file contains an employee’s salary. Update the employee’s salary.

19. Consider the following for loop:

```cpp
int j, s;

s = 0;
for (j = 1; j <= 10; j++)
    s = s + j * (j - 1);
```

In this for loop, identify the loop control variable, the initialization statement, the loop condition, the update statement, and the statement that updates the value of s.

20. What is the output of the following program segment?

```cpp
int num = 1;
int i;

for (i = 0; i < 5; i++)
{
    num = num * (5 - i);
    cout << num << " ";
}
cout << endl;
```

21. What is the output of the following program segment?

```cpp
int num = 0;
int count;
int y = 0;

for (count = 1; count <= 5; ++count)
{
    num = 3 * (count - 1) + (y - count);
    cout << num << " ";
}
cout << count << " " << endl;
```

22. Assume that the following code is correctly inserted into a program:

```cpp
int s = 0;
int i;

for (i = 0; i < 5; i++)
{
    s = 2 * s + i;
    cout << s << " ";
}
cout << endl;
```

- a. What is the final value of s?
  (i) 11          (ii) 4          (iii) 26          (iv) none of these

- b. If a semicolon is inserted after the right parenthesis in the for loop statement, what is the final value of s?
  (i) 0          (ii) 1          (iii) 2          (iv) 5          (v) none of these

- c. If the 5 is replaced with a 0 in the for loop control expression, what is the final value of s?
  (i) 0          (ii) 1          (iii) 2          (iv) none of these

23. State what output, if any, results from each of the following statements:

- a.
  ```cpp
  for (i = 1; i <= 1; i++)
      cout << "*";
  cout << endl;
  ```

- b.
  ```cpp
  for (i = 2; i >= 1; i++)
      cout << "*";
  cout << endl;
  ```

- c.
  ```cpp
  for (i = 1; i <= 1; i--)
      cout << "*";
  cout << endl;
  ```

- d.
  ```cpp
  for (i = 12; i >= 9; i--)
      cout << "*";
  cout << endl;
  ```

- e.
  ```cpp
  for (i = 0; i <= 5; i++)
      cout << "*";
  cout << endl;
  ```

- f.
  ```cpp
  for (i = 1; i <= 5; i++)
  {
      cout << "*";
      i = i + 1;
  }
  cout << endl;
  ```

24. Write a for statement to add all the multiples of 3 between 1 and 100.

25. What is the output of the following code? Is there a relationship between the variables x and y? If yes, state the relationship. What is the output?

```cpp
int x = 19683;
int i;
int y = 0;

for (i = x; i >= 1; i = i / 3)
    y++;
cout << "x = " << x << ", y = " << y << endl;
```

26. Suppose that the input is 5 3 8. What is the output of the following code? Assume all variables are properly declared.

```cpp
cin >> a >> b >> c;
for (j = 1; j < a; j++)
{
    d = b + c;
    b = c;
    c = d;
    cout << c << " ";
}
cout << endl;
```

27. What is the output of the following C++ program segment? Assume all variables are properly declared.

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

28. Suppose that the input is 3 5 7 -6 10. What is the output of the following code?

```cpp
int temp = 0;
int num;
int count;
```

- a.
  ```cpp
  x = 5;  y = 50;
  do
      x = x + 10;
  while (x < y);
  cout << x << " " << y << endl;
  ```

- b.
  ```cpp
  x = 5;  y = 80;
  do
      x = x * 2;
  while (x < y);
  cout << x << " " << y << endl;
  ```

- c.
  ```cpp
  x = 5;  y = 20;
  do
      x = x + 2;
  while (x >= y);
  cout << x << " " << y << endl;
  ```

- d.
  ```cpp
  x = 5;  y = 35;
  while (x < y)
      x = x + 10;
  cout << x << " " << y << endl;
  ```

- e.
  ```cpp
  x = 5;  y = 30;
  while (x <= y)
      x = x * 2;
  cout << x << " " << y << endl;
  ```

- f.
  ```cpp
  x = 5;  y = 30;
  while (x > y)
      x = x + 2;
  cout << x << " " << y << endl;
  ```

33. Write an input statement validation loop that prompts the user to enter a number less than 20 or greater than 75.

34. Rewrite the following as a for loop:

```cpp
int i = 0, value = 0;

while (i <= 20)
{
    if (i % 2 == 0 && i <= 10)
        value = value + i * i;
    else if (i % 2 == 0 && i > 10)
        value = value + i;
    else
        value = value - i;
    i = i + 1;
}

cout << "value = " << value << endl;
```

What is the output of this loop?

35. Write the while loop of Exercise 34 as a do...while loop.

36. The do...while loop in the following program is supposed to read some numbers until it reaches a sentinel (in this case, -1). It is supposed to add all of the numbers except for the sentinel. If the data looks like:

12    5    30    48    -1

The program does not add the numbers correctly. Correct the program so that it adds the numbers correctly.

```cpp
#include <iostream>

using namespace std;
int main()
{
    int total = 0,
        count = 0,
        number;
    do
    {
        cin >> number;
        total = total + number;
        count++;
    }
    while (number != -1);

    cout << "The number of data read is " << count << endl;
    cout << "The sum of the numbers entered is " << total
         << endl;

    return 0;
}
```

37. Using the same data as in Exercise 36, the following loop also fails. Correct it.

```cpp
cin >> number;
while (number != -1)
    total = total + number;
    cin >> number;
cout << endl;
cout << total << endl;
```

38. Using the same data as in Exercise 36, the following loop also fails. Correct it.

```cpp
cin >> number;
while (number != -1)
{
    cin >> number;
    total = total + number;
}
cout << endl;
cout << total << endl;
```

39. Given the following program segment:

```cpp
for (number = 1; number <= 10; number++)
    cout << setw(3) << number;
```

Write a while loop and a do...while loop that have the same output.
