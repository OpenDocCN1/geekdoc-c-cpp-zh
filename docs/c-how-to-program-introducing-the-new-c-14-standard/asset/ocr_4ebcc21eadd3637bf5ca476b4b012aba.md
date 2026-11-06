```
```cpp
// Fig. 22.44: fig22_44.cpp
// Using memcmp.
#include <iostream>
#include <iomanip>
#include <cstring> // memcmp prototype
using namespace std;

int main() {
   char s1[]{"ABCDFG"};
   char s2[]{"ABCDXYZ"};

   cout << "s1 = " << s1 << "\ns2 = " << s2 << endl
      << "\nmemcmp(s1, s2, 4) = " << setw(3) << memcmp(s1, s2, 4)
      << "\nmemcmp(s1, s2, 7) = " << setw(3) << memcmp(s1, s2, 7)
      << "\nmemcmp(s2, s1, 7) = " << setw(3) << memcmp(s2, s1, 7)
      << endl;
}
```
```

```
```text
s1 = ABCDFG
s2 = ABCDXYZ

memcmp(s1, s2, 4) =   0
memcmp(s1, s2, 7) =  -1
memcmp(s2, s1, 7) =   1
```
```

# Fig. 22.44 Memory-handling function `memcmp`.

Function `memchr` searches for the first occurrence of a byte, represented as `unsigned char`, in the specified number of bytes of an object. If the byte is found in the object, a pointer to it is returned; otherwise, the function returns a null pointer. Line 12 of **Fig. 22.45** searches for the character (byte) `'r'` in the string `"This is a string"`.