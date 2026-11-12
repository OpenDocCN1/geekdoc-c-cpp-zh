```
```cpp
int main()
{ S.f = 2;
    ((stud *)this)->fun(); }
```
```

+   - (a) 2
+   - (b) Error
+   - (c) Unpredictable
+   - (d) None of the above

**Answer:** (b) 'this' pointer can be used only inside a class.

125. What will be the error thrown by the code? (L5)

```
```cpp
#include<iostream>
using namespace std;
class stud
{ public:
    int f;
    void fun()
    { cout<<f; }
}S;
int main()
{ S.f = 2;
    ((stud *)this)->fun(); }
```
```

+   - (a) Invalid use of 'this' in non-member function
+   - (b) 'this' used in a non-member
+   - (c) 'this' usage doesn't map to a class
+   - (d) None of the above

**Answer:** (a) 'this' usage must be inside a member function only.

126. What is the output of the code? (L5)

```
```cpp
#include<iostream>
using namespace std;
class stud
{ public:
    int f;
}S;
class blo
{ public:
    void fun()
    { cout<<((stud *)this)->f; }
}D;
int main()
{ S.f = 2;
    D.fun(); }
```
```

+   - (a) 2
+   - (b) Error
+   - (c) Unpredictable
+   - (d) None of the above

**Answer:** (d) It prints '0'. This is because, '2' is given to specific object 'S'. But 'this' pointer calls the general function and not the specific to 'S'.

```
```cpp
int main()
{ cout<<"this in different class"; }
```
```

+   - (a) This is different class
+   - (b) Error
+   - (c) Unpredictable
+   - (d) None of the above

**Answer:** (a) 'this' pointer can also be used in a different and unrelated class.

127. What is the output of the code? (L5)

```
```cpp
#include<iostream>
using namespace std;
class stud
{ public:
    int f;
}S;
class blo
{ public:
    void fun()
    { cout<<((stud *)this)->f; }
}D;
int main()
{ S.f = 2;
    D.fun(); }
```
```

+   - (a) 2
+   - (b) Error
+   - (c) Unpredictable
+   - (d) None of the above

**Answer:** (d) It prints '0'. This is because, '2' is given to specific object 'S'. But 'this' pointer calls the general function and not the specific to 'S'.

128. What is the output of the code? (L5)

```
```cpp
#include<iostream>
using namespace std;
class stud
{ public:
    static int f;
}S;
int stud::f = 3;
class blo
{ public:
```
```