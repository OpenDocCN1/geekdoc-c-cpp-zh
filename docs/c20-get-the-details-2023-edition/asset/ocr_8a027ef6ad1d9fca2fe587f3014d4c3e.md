# 4.2.4 Further Aspects

# 4.2.4.1 Macros

Header units support macros, but modules ignore them. The following program consists of a module macro, a header macro.h used as header unit, and the main program macroMain.cpp.

The main program macroMain.cpp.

```
```cpp
// macroMain.cpp

#include <iostream>

import macro;
import "macro.h";

int main() {

    std::cout << '\n';

    std::cout << MACRO_HEADER_UNIT << '\n';
    std::cout << MACRO_MODULE << '\n';

    std::cout << '\n';
}
```
```

The program macroMain.cpp uses the two macros MACRO_HEADER_UNIT (line 12), and MACRO_MODULE (line 13). MACRO_MODULE_UNIT is defined in the header unit used header macro.h, and MACRO_MODULE in the module macro.

As the header unit used header macro.h.

```
```cpp
// macro.h

#define MACRO_HEADER_UNIT "macro header unit"
```
```