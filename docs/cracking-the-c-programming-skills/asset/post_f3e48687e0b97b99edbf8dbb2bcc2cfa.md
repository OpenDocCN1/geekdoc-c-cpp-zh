

**Answer: (d)** It throws `class base` is inaccessible. This is because static variables are not inherited.

- (a) 9 8
- (b) 9 0
- (c) Unpredictable
- (d) Error

**Answer: (a)** Even though two `public` blocks have been defined, both the blocks are inherited.

### 43. What will be the error thrown by the code? (L5)

```cpp
#include<iostream>
using namespace std;
class base
{ public:
      int b; };
class dev private base
{ public:
      void fun()
      { b = 2;
        cout<< b; }
};
int main()
{ D.fun(); }
```

- (a) Expected unqualified-id before `private`
- (b) Expected `:` or `{` before `private`
- (c) Invalid start of access block `private`
- (d) None of the above

**Answer: (a)** `:` is very important in inheritance.

### 45. What is the output of the code? (L4)

```cpp
#include<iostream>
using namespace std;
class base
{ public:
      int b;
  protected:
      int c; };
class dev : public, protected base
{ public:
      void fun()
      { b = 9;
        c = 7;
        cout<<b<< " "<<c; }
}D;
int main()
{ D.fun(); }
```

- (a) 9 7
- (b) Unpredictable
- (c) Error
- (d) None of the above

**Answer: (c)** A class cannot be inherited with multiple access modes.

### 44. What is the output of the code? (L4)

```cpp
#include<iostream>
using namespace std;
class base
{ public:
      int b;
  private:
      int v;
  public:
      int c; };
class dev : public base
{ }D;
int main()
{ D.b = 9;
  D.c = 8;
  cout<<D.b<< " "<<D.c; }
```

### 46. What will be the error thrown by the code? (L5)

```cpp
#include<iostream>
using namespace std;
class base
{ public:
      int b;
  protected:
      int c; };
class dev : public, protected base
{ public:
      void fun()
      { b = 9;
        c = 7;
        cout<<b<<" "<<c; }
}D;
int main()
{ D.fun(); }
```

- (a) Expected expression before ',' token in 'public, protected base'
- (b) Expected class name before ',' token in 'public, protected base'
- (c) Expected class-name before ',' token in 'public, protected base'
- (d) None of the above

**Answer:** (c) The compiler knows that class-name is required in the location according to inheritance syntax.

### 47. What is the output of the code? (L5)

```cpp
#include<iostream>
using namespace std;
class base
{ public:
    int b;};
class dev : base
{ public:
    void fun()
    { b = 9;
      cout<<b; }
}D;
int main()
{ D.fun(); }
```

- (a) 9
- (b) Unpredictable
- (c) Error
- (d) None of the above

**Answer:** (a) Even without access mode inheritance can be done.

### 48. What is the output of the code? (L5)

```cpp
#include<iostream>
using namespace std;
class base
{ public:
    int b;};
class dev : base
{ }D;
int main()
{ D.b = 3;
  cout<<D.b; }
```

- (a) 3
- (b) Unpredictable
- (c) Error
- (d) None of the above

**Answer:** (c) When the access mode is not specified it is inherited in 'private' mode.

### 49. What is the output of the code? (L4)

```cpp
#include<iostream>
using namespace std;
class dev : public base
{ public:
    int b;
    void fun()
    { b = 9;
      cout<<b; }
}D;
int main()
{ D.fun(); }
```

- (a) 9
- (b) Unpredictable
- (c) Error
- (d) None of the above

**Answer:** (c) Undefined class cannot be specified in inheritance. Here 'base' is unknown to the compiler.

### 50. What will be the error thrown by the code? (L5)

```cpp
#include<iostream>
using namespace std;
class dev : public base
{ public:
    int b;
    void fun()
    { b = 9;
      cout<<b; }
}D;
int main()
{ D.fun(); }
```

### 55. Which of the following will be a part of the error thrown by the code? (L5)

```cpp
#include<iostream>
using namespace std;
class dev : public class base
{ public:
    int b;
    void fun()
    { b = 9;
      cout<<b; }
}D;
int main()
{ D.fun(); }
```

- (a) Expected class-name before 'class' in 'dev: public class base'
- (b) Invalid type in declaration before ';' token in '}D;'
- (c) Both 'a' and 'b'
- (d) None of the above

**Answer:** (c) As the class has been marked wrong, its object cannot be declared. Thus 'b' is thrown.

### 56. What is the output of the code? (L3)

```cpp
#include<iostream>
using namespace std;
class base
{ public:
    void fun()
    { cout<<"fun"; }
};
class dev : public base
{ }D;
int main()
{ D.fun(); }
```

- (a) fun
- (b) Unpredictable
- (c) Error
- (d) None of the above

**Answer:** (a) Even functions will be inherited.

### 57. What is the output of the code? (L3)

```cpp
#include<iostream>
using namespace std;
class base
{ public:
    static void fun()
    { cout<<"fun"; }
};
class dev : public base
{ }D;
int main()
{ D.fun(); }
```

- (a) fun
- (b) Unpredictable
- (c) Error
- (d) None of the above

**Answer:** (a) Even static functions can be called like any normal functions.

### 58. What is the output of the code? (L3)

```cpp
#include<iostream>
using namespace std;
class base
{ public:
    static void fun()
    { cout<<"fun"; }
};
class dev : public base
{ }D;
int main()
{ dev::fun(); }
```

- (a) fun
- (b) Unpredictable
- (c) Error
- (d) None of the above

**Answer:** (a) This call is also allowed unlike 'static' variables.

### 59. What is the output of the code? (L3)

```cpp
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
}D;
int main()
{ D.fun(); }
```

- (a) fun1
- (b) fun2
- (c) Error
- (d) None of the above

**Answer:** (b) While there are two functions, derived class object calls the original function and not the inherited function.

### 60. What is the output of the code? (L3)

```cpp
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
}D;
int main()
{ D.base::fun(); }
```

- (a) fun1
- (b) fun2
- (c) Error
- (d) None of the above

**Answer:** (a) The base class function can be called using the derived class object by using '::' operator.

### 61. What is the output of the code? (L3)

```cpp
#include<iostream>
using namespace std;
class base
{ public:
    static void fun()
    { cout<<"fun1"; }
};
class dev : public base
{ public:
    static void funcall()
    { ((base *)this)->fun(); }
}D;
int main()
{ D.funcall(); }
```

- (a) fun1
- (b) fun2
- (c) Error
- (d) None of the above

**Answer:** (a) 'this' operator can also be used for calling the function.

### 62. What is the output of the code? (L4)

```cpp
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
}D;
int main()
{ D.fun(); }
```

- (a) 8
- (b) Prints nothing
- (c) Error
- (d) None of the above

**Answer:** (c) Same class cannot be inherited multiple times.

### 63. Which of the following will be a part of the error thrown by the code? (L5)

```cpp
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
}D;
int main()
{ D.fun(); }
```

- (a) Invalid base class
- (b) Duplicate base class 'base' invalid
- (c) Duplicate base type 'base' invalid
- (d) None of the above

**Answer:** (b) Along with this declaration of object is also thrown two more errors.

### 64. What is the output of the code? (L4)

```cpp
#include<iostream>
using namespace std;
class base
{ public:
    int b;
};
class base : public base
{ public:
    void fun()
    { b = 8;
      cout<<b; }
}D;
int main()
{ D.fun(); }
```

- (a) 8
- (b) Prints nothing
- (c) Error
- (d) None of the above

**Answer:** (c) A class can be defined only once.

### 65. Which of the following will be a part of the error thrown by the code? (L4)

```cpp
#include<iostream>
using namespace std;
class base
{ public:
    int b;
};
class base : public base
{ public:
    void fun()
    { b = 8;
      cout<<b; }
}D;
int main()
{ D.fun(); }
```

- (a) Duplicate class 'base'
- (b) Invalid base type 'base' for class 'base'
- (c) Both 'a' and 'b'
- (d) None of the above

**Answer:** (d) It throws an error "redefinition of 'class base'". Rest it has three more errors regarding the object 'D'.

### 66. What is the output of the code? (L2)

```cpp
#include<iostream>
using namespace std;
class base
{ public:
    int b;
};
class dev1
{ public:
    int c;
};
class dev2 : public base , public dev1
{ public:
    void fun()
    { b = 9;
      c = 2;
      cout<<b<<" "<<c; }
}D;
int main()
{ D.fun(); }
```

