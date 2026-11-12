```
~~~cpp
{ cout<<"fun1"; }
};
class dev : public base
{ public:
    static void fun()
    { cout<<"fun2"; }
};
int main()
{ D.fun(); }
~~~
```

+   - (a) fun1
+   - (b) fun2
+   - (c) Error
+   - (d) None of the above

Answer: (b) While there are two functions, derived class object calls the original function and not the inherited function.

60. What is the output of the code? (L3)

```
~~~cpp
#include<iostream>
using namespace std;
class base
{ public:
    static void fun()
    { cout<<"fun1"; }
};
class dev : public base
{ public:
    static void fun()
    { cout<<"fun2"; }
};
int main()
{ D.base::fun(); }
~~~
```

+   - (a) fun1
+   - (b) fun2
+   - (c) Error
+   - (d) None of the above

Answer: (a) The base class function can be called using the derived class object by using '::' operator.

61. What is the output of the code? (L3)

```
~~~cpp
#include<iostream>
using namespace std;
class base
{ public:
~~~
```

+   - (a) fun1
+   - (b) fun2
+   - (c) Error
+   - (d) None of the above

Answer: (c) Same class cannot be inherited multiple times.

```
~~~cpp
static void fun()
{ cout<<"fun1"; }
};
class dev : public base
{ public:
    static void funcall()
    { ((base *)this)->fun(); }
};
int main()
{ D.funcall(); }
~~~
```

+   - (a) fun1
+   - (b) fun2
+   - (c) Error
+   - (d) None of the above

Answer: (a) 'this' operator can also be used for calling the function.

62. What is the output of the code? (L4)

```
~~~cpp
#include<iostream>
using namespace std;
class base
{ public:
    int b;
};
class dev : public base , protected base
{ public:
    void fun()
    { b = 8;
      cout<<b; }
};
int main()
{ D.fun(); }
~~~
```

+   - (a) 8
+   - (b) Prints nothing
+   - (c) Error
+   - (d) None of the above

Answer: (c) Same class cannot be inherited multiple times.

63. Which of the following will be a part of the error thrown by the code? (L5)

```
~~~cpp
#include<iostream>
using namespace std;
class base
{ public:
~~~
```