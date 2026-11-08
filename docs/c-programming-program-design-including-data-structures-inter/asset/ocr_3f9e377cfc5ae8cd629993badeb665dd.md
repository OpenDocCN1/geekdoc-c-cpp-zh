```
12    5    30    48    -1
```

The program does not add the numbers correctly. Correct the program so that it adds the numbers correctly.

```
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

```
cin >> number;
while (number != -1)
    total = total + number;
    cin >> number;
cout << endl;
cout << total << endl;
```

38. Using the same data as in Exercise 36, the following loop also fails. Correct it.

```
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

```
for (number = 1; number <= 10; number++)
    cout << setw(3) << number;
```

Write a while loop and a do...while loop that have the same output.