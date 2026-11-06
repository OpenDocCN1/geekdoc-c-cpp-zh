# Considering the Effects of State

Application state is a condition that occurs when the application performs tasks that modify global data. An application doesn’t have state when using functional programming. The lack of state has the positive effect of ensuring that any call to a function will produce the same results for a given input every time, regardless of when the application calls the function. However, the lack of state has a negative effect as well: The application now has no memory. When you think about state, think about the capability to remember what occurred in the past, which, in the case of an application, is stored as global data.

Avoiding state in any C++ application is nearly impossible. A problem area is any sort of file or stream data, which by nature changes. The `FileLineCount` example, shown in Listing 1-4, demonstrates two techniques for determining the number of lines in a file named `Temp.txt`. The first method, `LineCount1()`, relies on state to track the current number of lines and the current character. The second method, `LineCount2()`, doesn’t directly contain any sort of tracking; theoretically, it has no state.

# LISTING 1-4: Avoiding the Use of State Directly

```
```cpp
#include <iostream>
#include <fstream>
#include <algorithm>

using namespace std;

int LineCount1(string filename) {
    int lineCount = 0;
    char c = ' ';

    ifstream thisFile(filename);

    while (thisFile.get(c)) {
        if (c == '\n')
            lineCount++;
    }

    thisFile.close();

    return lineCount;
}
```
```

*(continued)*