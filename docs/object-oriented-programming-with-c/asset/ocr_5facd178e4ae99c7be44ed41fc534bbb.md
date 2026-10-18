system can support. Program 15.4 illustrates how these characteristics are obtained and used in an application.

# Program 15.4 Obtaining String Characteristics

```
```cpp
#include <iostream>
#include <string>

using namespace std;

void display(string &str)
{
    cout << "Size = " << str.size() << "\\n";
    cout << "Length = " << str.length() << "\\n";
    cout << "Capacity = " << str.capacity() << "\\n";
    cout << "Maximum Size = " << str.max_size() << "\\n";
    cout << "Empty: " << (str.empty() ? "yes" : "no");
    cout << "\\n\\n";
}

int main()
{
    string str1;
    cout << "Initial status: \\n";
    display(str1);

    cout << "Enter a string (one word) \\n";
    cin >> str1;
    cout << "Status now: \\n";
    display(str1);

    str1.resize(15);
    cout << "Status after resizing: \\n";
    display(str1);
}
```
```