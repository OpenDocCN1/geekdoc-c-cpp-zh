# 11.6.4 Constructor That Specifies a MyArray’s Size

Line 16 of Fig. 11.4

`explicit MyArray(size_t size);` // constructor a MyArray of size elements declares a constructor that specifies the number of MyArray elements. The constructor’s definition (Fig. 11.5, lines 15–19) performs several tasks:

+   - Line 16 initializes the `m_size` member using the argument `size`.
+   - Line 17 initializes the `m_ptr` member to a `unique_ptr` returned by the standard library’s `make_unique` function template (see Section 11.5). Here, we use it to create a dynamically allocated int array of size elements. The function `make_unique` value initializes the dynamic memory it allocates, so the int array’s elements are set to 0.
+   - For pedagogic purposes, line 18 displays that the constructor was called. We do this in all of MyArray’s special member functions and other constructors to give you visual confirmation that the functions are being called.

```
```cpp
// Fig. 11.5: MyArray.cpp
// MyArray class member- and friend-function definitions.
#include <algorithm>
#include <format>
#include <initializer_list>
#include <iostream>
#include <memory>
#include <span>
#include <sstream>
#include <stdexcept>
#include <utility>
#include "MyArray.h"  // MyArray class definition

// MyArray constructor to create a MyArray of size elements containing 0
MyArray::MyArray(size_t size)
    : m_size{size},
      m_ptr{std::make_unique<int[]>(size)} {
    std::cout << "MyArray(size_t) constructor\n";
}
```
```

**Fig. 11.5** | MyArray class member- and friend-function definitions.

![](bbox=[0.139, 0.747, 0.174, 0.773])

# Checkpoint

1. (True/False) The function `make_unique` ______ the dynamic memory it allocates. Answer: value initializes.