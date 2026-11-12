# 22. What is the output of the code? (L3)

```
```cpp
#include<iostream>
using namespace std;
int main()
{ static int c = 9;
  cout<<sizeof(c); }
```
```

+   (a) 4　　　(b) 6
+   (c) Error　　(d) None of the above

**Answer: (a)** `static` storage class doesn’t affect the size of the variable. It just changes the storage properties of the variable.

# 23. What is the output of the code? (L2)

```
```cpp
#include<iostream>
using namespace std;
class sto
{ public:
    static int c;
};
int main()
{ S.c = 8;
  cout<<S.c; }
```
```

+   (a) 8　　　(b) 0
+   (c) Error　　(d) None of the above

**Answer: (c)** `static` member means, irrespective of the number of objects the member will be only one. It retains common value in a common memory. As it is not associated with any object it cannot be initiated with an object. It should be initiated only by using the class name with `::` operator.

# 24. What is the output of the code? (L3)

```
```cpp
#include<iostream>
using namespace std;
class sto
{ public:
    static int c = 8;
};
int main()
{ cout<<sto::c; }
```
```

+   (a) 8　　　(b) 0
+   (c) Error　　(d) None of the above

**Answer: (c)** Even though the static variable is common to the class, it cannot be initiated within the class.

# 25. What is the output of the code? (L2)

```
```cpp
#include<iostream>
using namespace std;
class sto
{ public:
    static int c;
};
int sto::c = 3;
int main()
{ cout<<sto::c; }
```
```

+   (a) 3　　　(b) 0
+   (c) Error　　(d) None of the above

**Answer: (a)** This is the way of initialising static variable.

# 26. What is the output of the code? (L2)

```
```cpp
#include<iostream>
using namespace std;
class sto
{ public:
    static int c;
};
int sto::c = 6;
int main()
{ cout<<S.c; }
```
```

+   (a) 6　　　(b) Unpredictable
+   (c) Error　　(d) None of the above

**Answer: (a)** Static variable can be read with separate objects also.

# 27. What is the output of the code? (L2)

```
```cpp
#include<iostream>
using namespace std;
class sto
{ public:
    static int c;
```
```