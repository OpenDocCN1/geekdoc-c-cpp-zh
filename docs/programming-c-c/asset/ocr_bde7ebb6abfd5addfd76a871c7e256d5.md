# Output:

```
Inside test_function
g = 25
s = 10
r = 5
Inside main
a = 17
g = 25
Inside test_function
g = 25
s = 20
r = 5
```

# 5. Mutable Storage Class

In C++, a class object can be kept constant using keyword const. This does not allow the data members of the class object to be modified during program execution. But, there are cases when some data members of this constant object must be changed. For example, during a bank transfer, a money transaction has to be locked such that no information could be changed but even then, its state has been changed from started to processing to completed. In those cases, we can make these modifiable using a mutable storage class.

# Syntax for Mutable Storage Class Declaration:

```
mutable datatype var_name1;
```

Example:

```
mutable int x;
mutable char y;
```

Example of Mutable Storage Class

Example 3: C++ program to create mutable variable.

```
#include<iostream>
using namespace std;
```