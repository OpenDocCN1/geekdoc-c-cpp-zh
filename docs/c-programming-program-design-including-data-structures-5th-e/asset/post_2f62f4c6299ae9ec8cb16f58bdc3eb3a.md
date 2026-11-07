
![](img/f97f778697507bb6fdd80c5991210cba_144_0.png)

### 13. Write each of the following as a C++ expression.

- a. 32 times a plus b
- b. The character that represents 8
- c. The string that represents the name `Julie Nelson`.
- d. `(b² − 4ac) / 2a`
- e. `(a + b) / (c − ef) − gh`
- f. `(-b + (b² − 4ac)) / 2a`

### 14. Suppose x, y, z, and w are `int` variables. What value is assigned to each of these variables after the last statement executes?

```cpp
x = 5; z = 3;
y = x - z;
z = 2 * y + 3;
w = x - 2 * y + z;
z = w - x;
w++;
```

### 15. Suppose x, y, and z are `int` variables and w and t are `double` variables. What value is assigned to each of these variables after the last statement executes?

```cpp
x = 17;
y = 15;
x = x + y / 4;
z = x % 3 + 4;
w = 17 / 3 + 6.5;
t = x / 4.0 + 15 % 4 - 3.5;
```

### 16. Suppose x, y, and z are `int` variables and x = 2, y = 5, and z = 6. What is the output of each of the following statements?

- a. `cout << "x = " << x << ", y = " << y << ", z = " << z << endl;`
- b. `cout << "x + y = " << x + y << endl;`
- c. `cout << "Sum of " << x << " and " << z << " is " << x + z << endl;`
- d. `cout << "z / x = " << z / x << endl;`
- e. `cout << "2 times " << x << " = " << 2 * x << endl;`

### 17. What is the output of the following statements? Suppose a and b are `int` variables, c is a `double` variable, and a = 13, b = 5, and c = 17.5.

- a. `cout << a + b - c << endl;`
- b. `cout << 15 / 2 + c << endl;`
- c. `cout << a / static_cast<double>(b) + 2 * c << endl;`
- d. `cout << 14 % 3 + 6.3 + b / a << endl;`
- e. `cout << static_cast<int>(c) % 5 + a - b << endl;`
- f. `cout << 13.5 / 2 + 4.0 * 3.5 + 18 << endl;`

### 18. Write C++ statements that accomplish the following.

- a. Output the newline character.
- b. Output the tab character.
- c. Output double quotation mark.

### 19. Which of the following are correct C++ statements?

- a. `cout << "Hello There!" << endl;`
- b.
  ```cpp
  cout << "Hello";
  << "There!" << endl;
  ```
- c.
  ```cpp
  cout << "Hello"
  << "There!" << endl;
  ```
- d. `cout << "Hello There!" << endl;`

### 20. Give meaningful identifiers for the following variables.

- a. A variable to store the first name of a student.
- b. A variable to store the discounted price of an item.
- c. A variable to store the number of juice bottles.
- d. A variable to store the number of miles traveled.
- e. A variable to store the highest test score.

### 21. Write C++ statements to do the following.

- a. Declare int variable num1 and num2.
- b. Prompt the user to input two numbers.
- c. Input the first number in num1 and the second number in num2.
- d. Output num1, num2, and 2 times num1 minus num2. Your output must identify each number and the expression.

### 22. The following program has syntax mistakes. Correct them. On each successive line, assume that any preceding error has been corrected.

```cpp
#include <iostream>

const int SECRET_NUM = 11,213;
const PAY_RATE = 18.35

main()
{
    int one, two;
    double first, second;
    one = 18;
    two = 11;

    first = 25;
    second = first * three;

    second = 2 * SECRET_NUM;
    SECRET_NUM = SECRET_NUM + 3;
    cout << first << " " << second << SECRET_NUM << endl;

    paycheck = hoursWorked * PAY_RATE

    cout << "Wages = " << paycheck << endl;
    return 0;
}
```

### 23. The following program has syntax mistakes. Correct them. On each successive line, assume that any preceding error has been corrected.

```cpp
const char = STAR = '*'
const int PRIME = 71;

int main
{
    int count, sum;
    double x;

    count = 1;
    sum = count + PRIME;
    x := 25.67;
    newNum = count * ONE + 2;
    sum + count = sum;
    x = x + sum * COUNT;
    cout << " count = " << count << ", sum = " << sum
         << ", PRIME = " << PRIME << endl;
}
```

### 24. The following program has syntax errors. Correct them. On each successive line, assume that any preceding error has been corrected.

```cpp
#include <iostream>

using namespace std;

int main()
{
    int temp;
    string first;

    cout << "Enter first name: ;
    cin >> first;
    cout << endl;

    cout << "Enter last name: ;
    cin >> last;
    cout << endl;

    cout << "Enter today's temperature: ";
    cin >> temperature;
    cout << endl;

    cout << first << " " << last << " today's temperature is: ";
         << temperature << endl;

    return 0;
}
```

### 25. What action must be taken before a variable can be used in a program?

### 26. Preprocessor directives begin with which of the following symbols:

- a. \*
- b. #
- c. $
- d. !
- e. None of these.

### 27. Write equivalent compound statements if possible.

- a. `x = 2 * x`
- b. `x = x + y − 2;`
- c. `sum = sum + num;`
- d. `z = z * x + 2 * z;`
- e. `y = y / (x + 5);`

### 28. Write the following compound statements as equivalent simple statements.

- a. `x += 5 − z;`
- b. `y *= 2 * x + 5 − z;`
- c. `w += 2 * z + 4;`
- d. `x −= z + y − t;`
- e. `sum += num;`

### 29. Suppose a, b, and c are int variables and a = 5 and b = 6. What value is assigned to each variable after each statement executes? If a variable is undefined at a particular statement, report UND (undefined).

| Statement | a | b | c |
|---|---|---|---|
| a = (b++) + 3; | ___ | ___ | ___ |
| c = 2 * a + (++b); | ___ | ___ | ___ |
| b = 2 * a + (++c) − (a++); | ___ | ___ | ___ |

### 30. Suppose a, b, and sum are int variables and c is a double variable. What value is assigned to each variable after each statement executes? Suppose a = 3, b = 5, and c = 14.1.

| Statement | a | b | c | sum |
|---|---|---|---|---|
| sum = a + b + c; | ___ | ___ | ___ | ___ |
| c /= a; | ___ | ___ | ___ | ___ |
| b += c − a; | ___ | ___ | ___ | ___ |
| a *= 2 * b + c; | ___ | ___ | ___ | ___ |

### 31. What is printed by the following program? Suppose the input is:

```
20 15
```

```cpp
#include <iostream>

using namespace std;

const int NUM = 10;
const double X = 20.5;

int main()
{
    int a, b;
    double z;
    char grade;

    a = 25;

    cout << "a = " << a << endl;

    cout << "Enter two integers: ";
    cin >> a >> b;
    cout << endl;

    cout << "The numbers you entered are "
         << a << " and " << b << endl;

    z = X + 2 * a - b;
    cout << "z = " << z << endl;

    grade = 'A';
    cout << "Your grade is " << grade << endl;

    a = 2 * NUM + z;
    cout << "The value of a = " << a << endl;

    return 0;
}
```

### 32. What is printed by the following program? Suppose the input is:

```
Miller
34
340
```

```cpp
#include <iostream>
#include <string>

using namespace std;

const int PRIME_NUM = 11;

int main()
{
    const int SECRET = 17;

    string name;
    int id;
    int num;
    int mysteryNum;

    cout << "Enter last name: ";
    cin >> name;
    cout << endl;

    cout << "Enter a two digit number: ";
    cin >> num;
    cout << endl;

    id = 100 * num + SECRET;

    cout << "Enter a positive integer less than 1000: ";
    cin >> num;
    cout << endl;

    mysteryNum = num * PRIME_NUM - 3 * SECRET;

    cout << "Name: " << name << endl;
    cout << "Id: " << id << endl;
    cout << "Mystery number: " << mysteryNum << endl;

    return 0;
}
```

### 33. Rewrite the following program so that it is properly formatted.

```cpp
#include <iostream>
#include <string>
using namespace std;
const double X = 13.45; const int Y=34;
const char BLANK=' ';
int main()
{string firstName,lastName;int num;
double salary;
cout<<"Enter first name: "; cin>> firstName; cout<<endl;
cout<<"Enter last name: "; cin
>>lastName;cout<<endl;
        cout<<"Enter a positive integer less than 70:";
cin>>num;cout<<endl; salary=num*X;
cout<<"Name: "<<firstName<<BLANK<<lastName<<endl; cout
<<"Wages: $"<<salary<<endl; cout<<"X = "<<X<<endl;
cout<<"X + Y = " << X+Y << endl; return 0;
}
```

### 34. What type of input does the following program require, and in what order does the input need to be provided?

```cpp
#include <iostream>

using namespace std;

int main()
{
    int age;
    double weight;
    string firstName, lastName;

    cin >> firstName >> lastName;
    cin >> age >> weight;

    return 0;
}
```
