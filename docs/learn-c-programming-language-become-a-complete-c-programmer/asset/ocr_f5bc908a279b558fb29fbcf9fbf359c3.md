```
double Parser::expr(bool get) { /* ... */ }
```

File **table.cpp** will look like this:

```
// table.cpp:
#include “dc.h”
```

**std::map<std::string,double> Table::table;** The symbol table is a standard-library **map**.

File **error.cpp** becomes:

```
// error.cpp:

#include “dg.h”
// anymore #includes or declarations
int Error::no_of_errors;
double Error::error(const string& s) { /* ... */ }
```

Finally, file **main.cpp** will look like this:

```
// main.cpp:

#include “dc.h”
#include <sstream>
#include <iostream> // redundant: in dc.h

void Driver::calculate() { /* ... */ }

int main(int argc, char * argv[]) { /* ... */ }
```

To be recognized as the **main()** of the program, **main()** must be a global function (§2.2.1, §15.4), so no namespace is used here.

The physical structure of the system can be presented like this:

```
<sstream> <map> <string> <cctype> <iostream>
dc.h
table .cpp parser.cpp main.cpp lexer.cpp error.cpp
```

The headers on the top are all headers for standard-library facilities. For many forms of program analysis, these libraries can be ignored because they are well known and stable. For tiny programs, the structure can be simplified by moving all **#include** directives to the common header. Similarly, for a small program, separating out **error.cpp** and **table.cpp** from **main.cpp** would often be excessive.

This single-header style of physical partitioning is most useful when the program is small and its parts are not intended to be used separately. Note that when namespaces are used, the logical structure of the program is still represented within **dc.h**. If namespaces are not used, the structure is obscured, although comments can be a help.

For larger programs, the single-header-file approach is unworkable in a conventional file-based development environment. A change to the common header forces recompilation of the whole program, and updates of that single header by several programmers are error-prone. Unless strong emphasis is placed on programming styles relying heavily on namespaces and classes, the logical structure deteriorates as the program grows.

# 15.3.2 Multiple-Header Organization