# Modern C++; Initialization In If And Switch Statements (C++17)

As a general principle, we should always restrict the scope of variables as much as possible.

In C++17, the if and switch syntax permit us to specify an initialization clause aside from the usual condition or switch clause. This will narrow the scope of the initialized variable to the control structure. For example, we can write:

```
if (int status = check(); status != 0) {
    return status;
}
```

this has a narrower scope than:

```
int status = check();
if (status != 0) {
    return status;
}
```

The initialization expression in this if statement is:

```
int status = check();
```

The status variable has scope from the beginning of the definition to the end of the if block, including an else block, if present.

Here is a complete example:

```
#include <iostream>

int test(int x) {
    if (x >= 0) return 1;
    return -1;
}

int main() {
{

```