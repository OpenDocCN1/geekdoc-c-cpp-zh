One improvement that has no deadlock and no starvation is to protect the five statements that follow the call to think by a mutex. Before starting to acquire forks, a philosopher would ask for a mutex. As we said earlier, mutex stands for mutual exclusion or the ability to provide exclusive access to some object. After replacing the forks, he would release the mutex. From a theoretical viewpoint, this approach is adequate. From a practical one, it has a performance issue: only one philosopher can eat at any instant of time. With five forks available, we should be able to allow two philosophers to eat at the same time.

The complete solution is given in the following example.

# Getting ready

Make sure Visual Studio is up to and running.

# How to do it...

+   1. Create a Win32 project. Name it PhilosophersDinner.
2. Open stafx.h and paste the following code:
```cpp
#pragma once
#include "targetver.h"
#define WIN32_LEAN_AND_MEAN
#include <windows.h>
#include <commctrl2.h>
#include <stdlib.h>
#include <malloc.h>
#include <memory.h>
#include <char.h>
#include <stdio.h>
#pragma comment ( lib, "comctl32.lib" )
#pragma comment ( linker, "/manifestdependency:type=win32' \\
name='Microsoft.Windows.Common-Controls' \\
version='6.0.0.0' processorArchitecture='*' \\
publicKeyToken='659b6414acccf1df' language='*' \"" )

#include "stafx.h"

#define BUTTON_CLOSE 100
#define PHILOSOPHER_COUNT 5
#define WM_INVALIDATE WM_USER + 1

typed struct _tagCOMMUNICATIONOBJECT
(
HND HWnd;
```

3. Open PhilosophersDinner.cpp and paste the following code:

![](bbox=[0.768, 0.837, 0.816, 0.853])