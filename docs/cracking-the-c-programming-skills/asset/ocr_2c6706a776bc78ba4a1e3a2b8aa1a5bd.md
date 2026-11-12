```
```cpp
{ public:
    int b;
    void fun()
    { a=1;
      base::b = 2;
      cout<<a<<" "<< b; }
};
int main()
{ D.fun(); }
```
```

+   (a) 1 2
+   
+   (b) Unpredictable
+   
+   (c) Error
+   
+   (d) None of the above

**Answer: (d)** Here ‘b’ is not initiated. Only the inherited variable is initialised—result is 1 0.

**28. What is the output of the code? (L2)**

```
```cpp
#include<iostream>
using namespace std;
class base
{ protected:
      int a,b; };
class dev : protected base
{ protected:
      int b;
   public:
      void fun()
      { a=1;
        base::b = 2;
        cout<<a<<" "<<b; }
};
int main()
{ D.fun(); }
```
```

+   (a) 1 2
+   
+   (b) Unpredictable
+   
+   (c) Error
+   
+   (d) None of the above

**Answer: (d)** Here ‘b’ is not initiated. Only the inherited variable is initialized—result is 1 0.

**29. What is the output of the code? (L2)**

```
```cpp
#include<iostream>
using namespace std;
class base
{ int b; };
class dev : protected base
{ public:
      void fun()
      { b = 2;
        cout<<b; }
};
int main()
{ D.fun(); }
```
```

+   (a) 2
+   
+   (b) Unpredictable
+   
+   (c) Error
+   
+   (d) None of the above

**Answer: (c)** ‘b’ is a private member of class ‘base’ so will not be inherited.

**30. What will be the error thrown by the code? (L4)**

```
```cpp
#include<iostream>
using namespace std;
class base
{ int b; };
class dev : protected base
{ public:
      void fun()
      { b = 2;
        cout<<b; }
};
int main()
{ D.fun(); }
```
```

+   (a) `int base::b` is private
+   
+   (b) `base::b` is inaccessible
+   
+   (c) Both ‘a’ and ‘b’
+   
+   (d) None of the above

**Answer: (a)** The compiler knows ‘b’ is a `private` variable of base class. As ‘dev’ is inherited from ‘base’ class the variable is in `private` of ‘base’.