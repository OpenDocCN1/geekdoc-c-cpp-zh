```
```cpp
using namespace std;

int main()
{
    string line;

    while (getline(cin, line))
    {
        reverse(line.begin(), line.end());
        cout << line << '\n';
    }
}
```
```

# 19.1.49  reverse_copy

+   - Header file: `<algorithm>`

+   - Function prototype:
+     - `OutputIterator reverse_copy(BidirectionalIterator first, BidirectionalIterator last, OutputIterator result);`

+   - Description:
+     - The elements in the range pointed to by `[first, last)` are copied to the range `[result, returnvalue)` in reversed order. The value returnvalue is the value that is returned by the function.

+   - Example:

```
```cpp
#include <algorithm>
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string line;

    while (getline(cin, line))
    {
        size_t    size = line.size();
        char      copy[size + 1];

        cout << "line: " << line << '\n' <<
                "reversed: ";
        reverse_copy(line.begin(), line.end(), copy);
        copy[size] = 0;        // 0 is not part of the reversed
                               // line !
        cout << copy << '\n';
    }
}
```
```

# 19.1.50  rotate

+   - Header file: `<algorithm>`