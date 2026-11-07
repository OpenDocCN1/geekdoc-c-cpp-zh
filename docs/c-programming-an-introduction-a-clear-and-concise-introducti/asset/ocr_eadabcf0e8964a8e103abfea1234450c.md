```
```cpp
return 0;
}
```
```

When you run this program, you first get a pop-up box with this message: "There were build errors. Would you like to continue and run the last successful build?" You should answer "No" to this question.

Now look at the bottom of Visual C++ Express, in the Output window. You will see the following message:

```
```text
1>------ Build started: Project: ErrorHandling.cpp, Configuration:
DebugWin32------
1>ErrorHandling.cpp
1> ErrorHandling.cpp(12): error C2143: Syntax error: missing ';' before
System::Console::ReadKey
======Build: 0 succeeded, 1 failed, 0 up-to-date, 0 skipped====
```
```

The Output message tells you very clearly that you have a missing semicolon and it also gives you the line where the compiler finally decided an error had occurred. It couldn't tell you the error was on line 11 because it had to wait to spot the following code on line 12 to be sure that the semicolon really needed to be placed at the end of line 11. However, Console::ReadKey() can't follow cout << "Hello, World!" << endl without there being a semicolon after the endl, so the error was reported.

Another common syntax error is to mistype the name of a variable. The following program demonstrates what happens when you type a variable name incorrectly:

```
```cpp
// ErrorHandling.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;
```
```