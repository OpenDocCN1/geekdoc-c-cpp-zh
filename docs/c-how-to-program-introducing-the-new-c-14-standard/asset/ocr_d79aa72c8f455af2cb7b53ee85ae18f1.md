from the second argument to a temporary array of characters, then copied from the temporary array to the first argument. This allows characters from one part of a string to be copied into another part of the same string.

![](bbox=[0.118, 0.251, 0.192, 0.303])

# Common Programming Error

# 22.11

*String-manipulation functions other than* `memmove` *that copy characters have undefined results when copying takes place between parts of the same string.*

The program in **Fig. 22.43** uses `memmove` (line 12) to copy the last `10` bytes of array `x` into the first `10` bytes of array `x`.

```
    // Fig. 22.43: fig22_43.cpp
    // Using memmove.
    #include <iostream>
    #include <cstring> // memmove prototype
    using namespace std;

    int main() {
       char x[] {"Home Sweet Home"};

       cout << "The string in array x before memmove is: " << x;
       cout << "\nThe string in array x after memmove is: "
            << static_cast<char*>(memmove(x, &x[5], 10)) << endl;
    }
```

```
The string in array x before memmove is: Home Sweet Home
The string in array x after memmove is: Sweet Home Home
```