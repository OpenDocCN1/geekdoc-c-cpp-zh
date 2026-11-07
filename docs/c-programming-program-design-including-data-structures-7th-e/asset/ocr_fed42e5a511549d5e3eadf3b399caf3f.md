function length. This is because the function length returns a value of the type `string::size_type`. Without the cast operator, some compilers might give the following warning message:

conversion from 'size_t' to 'unsigned int', possible loss of data

# EXAMPLE 7-15 (find FUNCTION)

Suppose `str1` and `str2` are of type `string`. The following are valid calls to the find function:

```
```cpp
str1.find(str2)
str1.find("the")
str1.find('a')
str1.find(str2 + "xyz")
str1.find(str2 + 'b')
```
```

Consider the following statements:

```
```cpp
string sentence = "Outside it is cloudy and warm.";
string str = "cloudy";

string::size_type position;
```
```

Next, we show the effect of the find function.

| Statement | Effect |
|---|---|
| `cout << sentence.find("is") << endl;` | Outputs 11 |
| `cout << sentence.find('s') << endl;` | Outputs 3 |
| `cout << sentence.find(str) << endl;` | Outputs 14 |
| `cout << sentence.find("the") << endl;` | Outputs the value of `string::npos` |
| `cout << sentence.find('i', 6) << endl;` | Outputs 8 |
| `position = sentence.find("warm");` | Assigns 25 to position |

Note that the search is case sensitive. Therefore, the position of o (lowercase o) in the string sentence is 16.

The following program evaluates the previous statements.

```
```cpp
//Example: find function

#include <iostream>
#include <string>

using namespace std;
```
```