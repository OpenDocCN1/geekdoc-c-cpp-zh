# **Program 13.7**  File smallest.h (Continued)

```
```cpp
#define SMALLEST_H
#include <iostream>
using namespace std;

class Smallest
{
private:
    int current;
public:
    Smallest();
    int operator() (int next); // function call operator
};
#endif
```
```

Program 13.8 shows the implementation of the class *Smallest*.
Program 13.9 shows the application file for testing the function object.

# **Program 13.8**  File smallest.cpp

```
```cpp
/************************************************************
 * The implementation file for the Smallest class           *
 ************************************************************/
#include "smallest.h"

// Constructor
Smallest :: Smallest ( )
{
    current = numeric_limits <int> :: max();
}
// Overloaded function call operator
int Smallest :: operator() (int next)
{
    if (next < current)
    {
        current = next;
    }
    return current;
}
```
```

# **Program 13.9**  File app.cpp

```
```cpp
/************************************************************
 * The application file to test the Smallest class          *
 ************************************************************/
```
```