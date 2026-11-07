In this code fragment, we declared num as an int variable and assigned it the value 100. We then declared ptrNum to be a pointer variable and we assigned it the address of num in the last statement. When referring to ptrNum, programmers commonly say that ptrNum points to num.

Now if we display the value of ptrNum, by writing:

```
cout << ptrNum;
```

we get this data:

```
0018ECF8
```

which is a memory address. This value will change every time you execute the statement.

If we want to see the value that is stored at this memory address, that is the value we stored in the num variable, we have to dereference the pointer variable, like this:

```
cout << *ptrNum;
```

This complete program illustrates what we've been discussing so far:

```
// pointerExample1.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;
```