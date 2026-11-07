![](bbox=[0.3125, 0.0893, 0.7363, 0.2407])

**Figure 13.9**  Overloading the subscript operator

# **Program 13.4**  File array.h

```
```cpp
/*******************************************************
 * The interface file for an Array class                 *
 *******************************************************/
#ifndef ARRAY_H
#define ARRAY_H
#include <iostream>
#include <cassert>
using namespace std;

class Array
{
    private:
        double* ptr;
        int size;
    public:
        Array (int size);  // Constructor
        ~Array();          // Destructor
        double& operator[ ] (int index) const; // Accessor
        double& operator[ ] (int index);       // Mutator
};
#endif
```
```

Program 13.5 shows the implementation file.

# **Program 13.5**  File Array.cpp

```
```cpp
/*******************************************************
 * The implementation file for Array class              *
 *******************************************************/
#include "array.h"
```
```

(continued)