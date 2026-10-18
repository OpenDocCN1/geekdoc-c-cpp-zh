```
```cpp
S1 = S2 + s3;
Cout << “S1 finally contains: “ << s1 << “\n”;
return 0;
}
```
```

The output of Program 15.1 would be:

```
```text
S1 = New
Now S1 = Standard C++ S4 = Standard C++
ENTER A STRING
COMPUTER CENTRE
Now S4 = COMPUTER

S1 finally contains: New Delhi
```
```

# 15.3  Manipulating String Objects

We can modify contents of **string** objects in several ways, using the member functions such as **insert()**, **replace()**, **erase()**, and **append()**. Program 15.2 demonstrates the use of some of these functions.

# Program 15.2  Modifying String Objects

```
```cpp
#include <iostream>
#include <string>

using namespace std;

int main()
{
string s1(“12345”);
```
```