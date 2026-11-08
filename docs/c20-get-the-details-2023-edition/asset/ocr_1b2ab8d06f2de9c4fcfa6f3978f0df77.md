# Definition of the function func

```
```cpp
// header.h

void func() {}
```
```

# Indirect inclusion of the function definition to func

```
```cpp
// header2.h

#include "header.h"
```
```

# Double definitions of the function func

```
```cpp
// main.cpp

#include "header.h"
#include "header2.h"

int main() {}
```
```

The linker complains about the multiple definitions of func:

![](bbox=[0.2, 0.552, 0.799, 0.769])

Breaking the one definition rule

We are used to ugly workarounds, such as putting an include guard around your header. Adding the include guard FUNC_H to the header file header.h solves the issue.