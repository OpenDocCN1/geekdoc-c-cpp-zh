```
```cpp
value = value + i;
else
    value = value - i;
i = i + 1;
}

cout << "value = " << value << endl;
```
```

What is the output of this loop?

35. Write the while loop of Exercise 34 as a do...while loop. (2, 5)

36. The do...while loop in the following program is supposed to read some numbers until it reaches a sentinel (in this case, -1). It is supposed to add all of the numbers except for the sentinel. If the data looks like: (5)

12    5    30    48    -1

the program does not add the numbers correctly. Correct the program so that it adds the numbers correctly.

```
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
```

37. Using the same data as in Exercise 36, the following loop also fails. Correct it. (2)

```
```cpp
cin >> number;
while (number != -1)
    total = total + number;
    cin >> number;
    cout << endl;
    cout << total << endl;
```
```