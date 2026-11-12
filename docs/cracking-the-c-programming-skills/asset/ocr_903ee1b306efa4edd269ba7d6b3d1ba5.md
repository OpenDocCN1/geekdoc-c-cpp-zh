Answer: (a) Redeclaration of variable inside the class is not possible.

# 33. What is the output of the code? (L3)

```
```cpp
#include<iostream>
using namespace std;
class student
{ public:
int m;
int ;
}S;
int main()
{ cout<<sizeof(S); }
```
```

(a) 8          (b) 4
(c) Error      (d) None of the above

**Answer:** (c) Type cannot be given separately inside class for declaration.

# 34. What will be the error thrown by the code? (L3)

```
```cpp
#include<iostream>
using namespace std;
class student
{ public:
int m;
int ;
}S;
int main()
{ cout<<sizeof(S); }
```
```

(a) Invalid declaration [-rpermissive]
(b) Declaration does not declare anything [-fpermissive]
(c) Expected expression before ',' '
(d) None of the above

**Answer:** (b) Type cannot be given separately inside class for declaration.

# 35. What is the output of the code? (L3)

```
```cpp
#include<iostream>
using namespace std;
class student
{ }S;
int student::m;
int main()
{ S.m=8;
cout<<S.m; }
```
```

(a) 8          (b) Error
(c) unpredictable (d) None of the above

**Answer:** (b) This declaration of members is not possible.

# 36. What will be the error thrown by the code? (L4)

```
```cpp
#include<iostream>
using namespace std;
class student
{ }S;
int student::m;
int main()
{ S.m=8;
cout<<S.m; }
```
```

(a) 'int student::m' is not a static member of 'class student'
(b) 'class student' has no member named 'm'
(c) Class member declared as non-static
(d) Both 'a' and 'b'
(e) Both 'b' and 'c'

**Answer:** (d) This is not allowed. This has a different meaning. It is related with 'static' members of class. This will be discussed in later chapters.

# 37. What is the output of the code? (L3)

```
```cpp
#include<iostream>
using namespace std;
class student
{ public:
int m;
}S;
S.m;
int main()
{ S.m=8;
cout<<S.m; }
```
```