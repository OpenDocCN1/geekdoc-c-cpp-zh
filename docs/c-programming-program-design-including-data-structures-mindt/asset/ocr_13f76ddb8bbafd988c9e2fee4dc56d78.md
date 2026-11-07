30. Suppose a, b, and sum are int variables and c is a double variable. What value is assigned to each variable after each statement executes? Suppose a = 6, b = 3, and c = 2.2. (14)

| Statement | a | b | c | sum |
| --- | --- | --- | --- | --- |
| sum = static_cast<int>(a + b + c); | — | — | — | — |
| b += c * a; | — | — | — | — |
| c -= a; | — | — | — | — |
| a *= 2 * b - c; | — | — | — | — |

31. What is printed by the following program? Suppose the input is:

35 10.5 27 B

```
~~~cpp
#include <iostream>

using namespace std;

const int NUM = 10;
const double X = 20.5;

int main()
{
    int firstNum, secondNum;
    double z;
    char grade;

    firstNum = 62;

    cout << "firstNum = " << firstNum << endl;

    cout << "Enter three numbers: ";
    cin >> firstNum >> z >> secondNum;
    cout << endl;

    cout << "The numbers you entered are "
         << firstNum << ", " << z << ", and "
         << secondNum << endl;

    z = z - X + 2 * firstNum - secondNum;
    cout << "z = " << z << endl;

    cout << "Enter grade: ";
    cin >> grade;
    cout << endl;

    cout << "The letter that follows your grade is: "
         << static_cast<char>(static_cast<int>(grade) + 1)
         << endl;

    return 0;
}
~~~
```