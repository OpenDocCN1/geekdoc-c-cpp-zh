```
c.  cin >> y;
    cin.ignore(100, '\n');
    cin >> x >> symbol;

d.  cin.get(symbol);
    cin.ignore(100, '*');
    cin >> x;
    cin.ignore(100, '\n');
    cin >> y;

e.  cin.ignore(100, '\n');
    cin >> x >> symbol;
    cin.ignore(100, '&');
    cin >> y;
```

5. Given the input:

```
46 A 49
```

and the C++ code:

```
int x = 10, y = 18;
char z = 'A';
cin >> x >> y >> z;
cout << x << " " << y << " " << z << endl;
```

What is the output?

6. Suppose that x and y are int variables, z is a double variable, and ch is a char variable. Suppose the input statement is:

```
cin >> x >> y >> ch >> z;
```

What values, if any, are stored in x, y, z, and ch if the input is:

+   a. 35 62.78
+   b. 86 32A 92.6
+   c. 12 .45A 32

7. Which header file must be included to use the function setprecision()?

8. Which header file must be included to use the function pow?

9. Which header file must be included to use the function sqrt?

10. What is the output of the following program?

```
#include <iostream>
#include <cmath>
#include <string>

using namespace std;
```