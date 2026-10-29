namespaces in detail later in this book. For now, we only need to discuss the namespace std. All the standard libraries we will be using are defined in the std (standard) namespace. To use any of these definitions in your program, you must insert the following using directive:

```
using namespace std;
```

Thus, a simple program that uses console I/O would begin

```
#include <iostream>
using namespace std;
```

If you want to make some, but not all, names in a namespace available to your program, there is a form of the using directive that makes just one name available. For example, if you only want to make the name cin from the std namespace available to your program, you could use the following using directive:

```
using std::cin;
```

Thus, if the only names from the std namespace that your program uses are cin, cout, and endl, you might start your program with

```
#include <iostream>
using std::cin;
using std::cout;
using std::endl;
```

instead of

```
#include <iostream>
using namespace std;
```

Older C++ header files for libraries did not place their definitions in the std namespace, so if you look at older C++ code, you will probably see that the header file names are spelled slightly differently and the code does not contain any using directive. This is allowed for backward compatibility. However, you should use the newer library header files and the std namespace directive.

# PITFALL: Problems with Library Names

The C++ language is constantly in transition. If you are using a compiler that has not yet been revised to meet the new standard, then you will need to use different library names.

If the following does not work

```
#include <iostream>
```

```
use
```

```
#include <iostream.h>
```