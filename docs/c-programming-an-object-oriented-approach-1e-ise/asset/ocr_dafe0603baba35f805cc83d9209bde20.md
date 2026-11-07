# PR-9. What is printed from the following program?

```
```cpp
#include <iostream>
using namespace std;

void fun (int& y);

int main ()
{
    fun (10);

    cout << x << endl;
    return 0;
}

void fun (int& y)
{
    y++;
}
```
```

# PR-10. What is printed from the following program?

```
```cpp
#include <iostream>
using namespace std;

int& fun (int& yy, int& zz);

int main ()
{
    int x = 120;
    int y = 80;
    cout << fun (x, y);
    return 0;
}

int& fun (int& yy, int& zz)
{
    if (yy > zz)
    {
        return yy;
    }
    return zz;
}
```
```

# PR-11. What is printed from the following program?

```
```cpp
#include <iostream>
using namespace std;

int& fun (int yy, int zz);
```
```