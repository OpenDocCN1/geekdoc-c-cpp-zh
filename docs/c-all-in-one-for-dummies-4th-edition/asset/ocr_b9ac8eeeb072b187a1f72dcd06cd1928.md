+   15. **Type the location of the Boost library files in the Directory field and then click OK.**
+   
+   The Boost library files are typically located in the `\CodeBlocks\boost_1_73_0\bin.v2\libs` directory. After you click OK, you see the directory added to the Linker tab.

+   16. **Click OK.**
+   
+   The selected library is ready for inclusion in your application.

# Creating the RegEx code

Using a regular expression is relatively straightforward. All you do is create the expression and then use it with a function to perform specific kinds of pattern matches. The function you choose is important because each function performs the pattern matching differently. The RegEx example code, shown in Listing 5-1, demonstrates how to create a regular expression and then use it in two different ways to determine whether user input is correct.

# **LISTING 5-1:** Performing Matches and Searches Using RegEx

```
```cpp
#include <iostream>
#include "boost/regex.hpp"

using namespace std;
using namespace boost;

int main() {
    char MyNumber[80];
    cout << "Type a three-digit number: ";
    cin >> MyNumber;

    regex Expression("[0-9][0-9][0-9]");
    cmatch Matches;

    // Perform a matching check.
    if (regex_match(MyNumber, Matches, Expression)) {
        cout << "You typed: " << Matches << endl;
    } else {
        cout << "Not a three-digit number!" << endl;
    }
}
```
```

*(continued)*