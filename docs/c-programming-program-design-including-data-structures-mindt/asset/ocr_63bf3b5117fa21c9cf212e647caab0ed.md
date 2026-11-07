```
```cpp
else
{
    num = -num;
    num = static_cast<int>(sqrt(num * 1.0));
}
cout << num << endl;
```
```

+   a. What is the output if the input is 7?
+   
+   b. What is the output if the input is 23?
+   
+   c. What is the output if the input is 20?
+   
+   d. What is the output if the input is -9?

30. In the following code, without adding new statements, correct any errors that would prevent the program from compiling or running. (3, 11)

```
```cpp
#include <iostream>

using namespace;

int main
{
    int num1, num2;
    bool found = false;

    cout << "Enter two integers: ";
    cin >> num1 >> num2;
    cout << endl;

    found = (num1 > num2);

    if (found
        switch (num1 % num2);
        {
        case 0:
            num2 = num1 / 2;
            break;
        case 1:
            num1 = num2 / 2;
            break;
        default:
            num1 = num1 / num2;
            num2 = num1 * num2;
        };
    else
    {
        num1 = num1 - num2;
        num2 = (num1 + num2) / 10;
    }

    cout << num1 << " " << num2 << endl;

    return;
}
```
```