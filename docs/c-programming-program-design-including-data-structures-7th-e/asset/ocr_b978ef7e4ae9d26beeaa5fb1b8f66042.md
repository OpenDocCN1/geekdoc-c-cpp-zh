| | a | b | c | sum |
|---|---|---|---|---|
| sum = a + b + c; | ___ | ___ | ___ | ___ |
| c /= a; | ___ | ___ | ___ | ___ |
| b += c - a; | ___ | ___ | ___ | ___ |
| a *= 2 * b + c; | ___ | ___ | ___ | ___ |

31. What is printed by the following program? Suppose the input is: (8, 10, 11)

35 10.5 27 B

```
```cpp
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
```
```

32. What is printed by the following program? Suppose the input is: (8, 10, 11)

Miller
34
62.5