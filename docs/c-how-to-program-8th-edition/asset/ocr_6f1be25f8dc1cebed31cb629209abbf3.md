```
```cpp
// Fig. 21.42: fig21_42.cpp
// Using memcpy.
#include <iostream>
#include <cstring> // memcpy prototype
using namespace std;

int main()
{
   char s1[17];

   // 17 total characters (includes terminating null)
   char s2[] = "Copy this string";

   memcpy( s1, s2, 17); // copy 17 characters from s2 to s1

   cout << "After s2 is copied into s1 with memcpy,\n"
        << "s1 contains \"" << s1 << "\"\n" << endl;
} // end main
```
```

```
```text
After s2 is copied into s1 with memcpy,
s1 contains "Copy this string"
```
```

**Fig. 21.42** | Memory-handling function memcpy.

Function **memmove**, like **memcpy**, copies a specified number of bytes from the object pointed to by its second argument into the object pointed to by its first argument. Copying is performed as if the bytes were copied from the second argument to a temporary array of characters, then copied from the temporary array to the first argument. This allows characters from one part of a string to be copied into another part of the same string.

![](bbox=[0.159, 0.604, 0.219, 0.646])

> > **Common Programming Error 21.11**
> >
> > *String-manipulation functions other than memmove that copy characters have undefined results when copying takes place between parts of the same string.*

The program in Fig. 21.43 uses **memmove** (line 13) to copy the last 10 bytes of array x into the first 10 bytes of array x.

```
```cpp
// Fig. 21.43: fig21_43.cpp
// Using memmove.
#include <iostream>
#include <cstring> // memmove prototype
using namespace std;

int main()
{
   char x[] = "Home Sweet Home";

   cout << "The string in array x before memmove is: " << x;
   cout << "\n\nThe string in array x after memmove is:  "
```
```

**Fig. 21.43** | Memory-handling function memmove. (Part 1 of 2.)