```
```cpp
// Fig. 7.5: fig07_05.cpp
// Set array s to the even integers from 2 to 10.
#include <iostream>
#include <iomanip>
#include <array>
using namespace std;

int main()
{
   // constant variable can be used to specify array size
   const size_t arraySize = 5; // must initialize in declaration

   array<int, arraySize> s; // array s has 5 elements

   for (size_t i = 0; i < s.size(); ++i) // set the values
      s[i] = 2 * i + 2;

   cout << "Element" << setw(13) << "Value" << endl;

   // output contents of array s in tabular format
   for (size_t j = 0; j < s.size(); ++j)
      cout << setw(7) << j << setw(13) << s[j] << endl;
} // end main
```
```

| Element | Value |
|---:|---:|
| 0 | 2 |
| 1 | 4 |
| 2 | 6 |
| 3 | 8 |
| 4 | 10 |

**Fig. 7.5**  |  Set array s to the even integers from 2 to 10.

expression when it’s declared and **cannot** be modified thereafter (as shown in Fig. 7.6 and Fig. 7.7). Constant variables are also called **named constants** or **read-only variables**.

> **Common Programming Error 7.2**
> 
> _Not initializing a constant variable when it’s declared is a compilation error._

> **Common Programming Error 7.3**
> 
> _Assigning a value to a constant variable in an executable statement is a compilation error._

```
```cpp
// Fig. 7.6: fig07_06.cpp
// Using a properly initialized constant variable.
#include <iostream>
using namespace std;

int main()
{
```
```

**Fig. 7.6**  |  Using a properly initialized constant variable. (Part 1 of 2.)