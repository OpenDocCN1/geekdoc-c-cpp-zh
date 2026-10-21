# Chapter 2

![](bbox=[0.17, 0.09, 0.77, 0.46])

Figure 2-13

When you click on the OK button, the Application Wizard will generate the project containing the following code:

```
// Ex2_12.cpp : main project file.

#include "stdafx.h"

using namespace System;

int main(array<System::String ^> ^args)
{
    Console::WriteLine(L"Hello World");
    return 0;
}
```

I’m sure you’ve noticed the extra stuff between the parentheses following main. This is concerned with passing values to the function main() when you initiate execution of the program from the command line, and you’ll learn more about this when you explore functions in detail. If you compile and execute the default project, it will write "Hello World" to the command line. Now, you’ll convert this program to a CLR version of Ex2_02 so you can see how similar it is. To do this, you can modify the code in Ex2_12.cpp as follows:

```
// Ex2_12.cpp : main project file.
#include "stdafx.h"
```