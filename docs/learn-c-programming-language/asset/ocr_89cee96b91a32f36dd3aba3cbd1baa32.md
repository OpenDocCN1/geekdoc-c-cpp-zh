```
```cpp
}
```
```

If we compile and run above code, this would produce the following result:

```
```
HELLO C++
```
```

Let us see how it worked. It is simple to understand that the C++ preprocessor turns the line:

```
```cpp
cout << MKSTR(HELLO C++) << endl;
```
```

Above line will be turned into the following line:

```
```cpp
cout << "HELLO C++" << endl;
```
```

The ## operator is used to concatenate two tokens. Here is an example:

```
```cpp
#define CONCAT( x, y )  x ## y
```
```

When CONCAT appears in the program, its arguments are concatenated and used to replace the macro. For example, CONCAT(HELLO, C++) is replaced by "HELLO C++" in the program as follows.

```
```cpp
#include <iostream>

using namespace std;

#define concat(a, b) a ## b
int main()
{
    int xy = 100;

    cout << concat(x, y);
    return 0;
}
```
```

If we compile and run above code, this would produce the following result:

```
```
100
```
```

Let us see how it worked. It is simple to understand that the C++ preprocessor transforms:

```
```cpp
cout << concat(x, y);
```
```