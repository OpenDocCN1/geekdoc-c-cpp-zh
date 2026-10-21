```
#define NDEBUG                // Switch off assertions in the code
#include <cassert>              // Declares assert()
```

If the expression passed as an argument to assert() is non-zero (i.e. true) the function does nothing. If the expression is 0 (false in other words) and NDEBUG are not defined, a diagnostic message is output showing the expression that failed, the source file name, and the line number in the source file where the failure occurred. After displaying the diagnostic message, the assert() function calls abort() to end the program. Here’s an example of an assertion used in a function:

```
char* append(char* pStr, const char* pAddStr)
{
```

```
// Verify non-null pointers
assert(pStr != 0);
assert(pAddStr != 0);
```

```
// Code to append pAddStr to pStr...
}
```

Calling the append() function with a null pointer argument in a simple program produced the following diagnostic message on my machine:

```
Assertion failed: pStr != 0, file c:\beginning visual c++.net\examples\testassert\
testassert \ testassert.cpp, line 11
```

The assertion also displays a message box offering you the three options shown in Figure 10-10.

![](bbox=[0.3, 0.54, 0.81, 0.74])

Figure 10-10

Clicking the Abort button ends the program immediately. The Retry button starts the Visual C++ 2005 debugger so you can step through the program to find out more about why the assertion failed. In principle, the Ignore button allows the program to continue in spite of the error, but this is usually an unwise choice as the results are likely to be unpredictable.