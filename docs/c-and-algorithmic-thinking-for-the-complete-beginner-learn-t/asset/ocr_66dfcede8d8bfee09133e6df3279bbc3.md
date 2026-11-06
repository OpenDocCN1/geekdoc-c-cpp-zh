Let’s say that user’s input is assigned to variable `str`. You can access the fourth letter using `str.at(3)`, the third letter using `str.at(2)`, and so on.

The C++ program is shown here.

```
**project_14_3_1**

```cpp
#include <iostream>
using namespace std;
int main() {
    string str;

    cout << "Enter a word with four letters: ";
    cin >> str;

    cout << str.at(3) << str.at(2) << str.at(1) << str.at(0);
    return 0;
}
```
```

# 14.4 Useful String Functions

# Trimming

Trimming is the process of removing whitespace characters from the beginning or the end of a string.

Some of the whitespace characters that are removed with the trimming process are:

+   - `" "` an ordinary space
+   - `"\t"` a tab
+   - `"\n"` a new line (line feed)
+   - `"\r"` a carriage return

For example, you can trim any spaces that the user mistakenly entered at the end of a string.

The function that you can use to trim a string is

```
```cpp
trim_copy(subject)
```
```

This removes any whitespace characters from both the beginning and the end of `subject`. It is defined in the boost library.

**Example**

```
**project_14_4a**

```cpp
#include <iostream>
#include <boost/algorithm/string.hpp>
using namespace boost::algorithm;
using namespace std;
int main() {
    string a, b;

    a = "        Hello        ";
    b = trim_copy(a);
}
```
```