# Listing 4.4: reformattedvariable.cpp

```
#include <iostream>
int
main
(
)
{
{
int
x
;
x
=
10
;
std
:
:
cout
<<
x
<<
'\n'
;
}
}
}
```

Listing 4.5 (reformattedvariable2.cpp) is another reformatted version of Listing 3.4 (variable.cpp).

# Listing 4.5: reformattedvariable2.cpp

```
#include <iostream>
int main(){int x=10;std::cout<<x<<'\n';}
```

Both reformatted programs are valid C++ and compile to the same machine language code as the original version. Most would argue that the original version is easier to read and understand more quickly than either of the reformatted versions. The elements in Listing 3.4 (variable.cpp) are organized better. Experienced C++ programmers would find both Listing 4.4 (reformattedvariable.cpp) and Listing 4.5 (reformattedvariable2.cpp) visually painful.

What are some distinguishing characteristics of Listing 3.4 (variable.cpp)?

+   - Each statement appears on its own line. A statement is not unnecessarily split between two lines of text. Visually, one line of text implies one action (statement) to perform.
+   - The close curly brace aligns vertically with the line above that contains the corresponding open curly brace. This makes it easier to determine if the curly braces match and nest properly. It also better portrays the logical structure of the program. The ability to accurately communicate the logical structure of a program becomes very important as write more complex programs. Programs with complex logic frequently use multiple nested curly braces (for example, see Listing 5.12 (troubleshoot.cpp)). Without a consistent, organized arrangement of curly braces it can difficult to determine which opening brace goes with a particular closing brace.
+   - The statements that constitute the body of main are indented several spaces. This visually emphasizes the fact that the elements are indeed logically enclosed. As with curly brace alignment, indentation to emphasize logical enclosure becomes more important as more complex programs are considered.