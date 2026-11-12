
### （续）

```cpp
}
};
int main()
{
    Base_class obj1;
    Base_class *p;
    p = &obj1;
    p->show();
    Derived_class obj2;
    p = &obj2;
    p->show();
    Derived_class_2 obj3;
    p = &obj3;
    p->show();
    return 0;
}
```

- (a) Virtual keyword is used wrongly
- (b) Function Show in Base Class  
  Function Show in derived Class  
  Function Show in derived Class_2
- (c) Function Show in derived Class  
  Function Show in derived Class_2
- (d) None of the above

**Answer:** (b) Virtual once used in the base class will be valid all over the code.

### （续）

```cpp
cout << "Function Show in derived class" << endl;
}
};
int main()
{
    Base_class obj1;
    Base_class *p;
    p = &obj1;
    p->show();
    Derived_class obj2;
    p = &obj2;
    p->show();
    return 0;
}
```

- (a) Compilation error
- (b) Show() cannot be empty in the base class
- (c) Function Show in derived Class
- (d) None of the above

**Answer:** (c) The statement in the derived class will get printed as the function in the base class is referred as “Pure Virtual Function”. The function in the derived class will be re-defined in the derived class.

### 57. What is the output of the following piece of code? (L4)

```cpp
#include <iostream>
using namespace std;
class Base_class
{
public:
    virtual void show()
    {
    }
};
class Derived_class : public Base_class
{
public:
    void show()
    {
```

### 58. What is the output of the following piece of code?

```cpp
#include <iostream>
using namespace std;
class Base_class
{
public:
    virtual void show()
    {
    }
};
class Derived_class : public Base_class
{
public:
    void show()
    { }
};
int main()
```

- (a) Compilation fault
- (b) No error. No output
- (c) Illegal not to override the function in derived class, when the base class function is virtual
- (d) None of the above

**Answer:** (b) No error and no output as the function in derived class has got nothing inside.

### 59. What is the output of the following piece of code? (L4)

```cpp
#include <iostream>
using namespace std;
class Base_class
{
public:
    virtual void show()
    { }
};
class Derived_class : public Base_class
{
public:
    virtual void show()
    { }
};
int main()
{
    Base_class obj1;
    Base_class *p;
    p = &obj1;
    p->show();
    Derived_class obj2;
    p = &obj2;
    p->show();
    return 0;
}
```

- (a) Compilation fault
- (b) No error. No output
- (c) Illegal as a function cannot be made virtual in base and derived classes
- (d) None of the above

**Answer:** (b) No error and no output and it is not harmful to have same function virtual in both base and derived classes.

### 60. What is the output of the following piece of code? (L4)

```cpp
#include <iostream>
using namespace std;
class Base_class
{
public:
    virtual void show() = 0;
};
class Derived_class : public Base_class
{
public:
    virtual void show()
    {
        cout << "hi" << " this is a demo for pure virtual function";
    }
};
int main()
{
    Base_class *p;
    Derived_class obj2;
    p = &obj2;
    p->show();
    return 0;
}
```

- (a) Compilation fault
- (b) No error. No output
- (c) This is a demo for pure virtual function
- (d) None of the above

**Answer:** (c) This is demo for pure virtual function as the base class virtual function equated to zero and has been overridden in the derived class.

### 61. What is the output of the following piece of code? (L4)

```cpp
#include <iostream>
using namespace std;
class Base_class
{
public:
    virtual void show() = 0;
};
class Derived_class : public Base_class
{
public:
    virtual void show()
    {
        cout << "\n" << " This is a demo for pure virtual function";
    }
};
int main()
{
    Base_class *p;
    Derived_class obj2;
    p = &obj2;
    p->show();
    return 0;
}
```

- (a) Compilation fault
- (b) No error. No output
- (c) This is a demo for pure virtual function
- (d) None of the above

**Answer:** (c) This is demo for pure virtual function as the base class virtual function is equated to zero and has been overridden in the derived class.

### 62. What is the output of the following piece of code? (L4)

```cpp
#include <iostream>
using namespace std;
class Base_class
{
public:
    virtual void show() = NULL;
};
class Derived_class : public Base_class
{
public:
    virtual void show()
    {
        cout << "\n" << " This is a demo for pure virtual function";
    }
};
int main()
{
    Base_class *p;
    Derived_class obj2;
    p = &obj2;
    p->show();
    return 0;
}
```

- (a) Compilation fault
- (b) No error. No output
- (c) This is a demo for pure virtual function
- (d) None of the above

**Answer:** (a) Compilation error as NULL is invalid pure specifier. Only 0 is preferred as pure specifier.

### 63. What is the output of the following piece of code? (L4)

```cpp
#include <iostream>
using namespace std;
class Base_class
{
public:
    virtual void show() = "ZERO";
```

- (a) Compilation fault
- (b) No error. No output
- (c) This is a demo for pure virtual function
- (d) None of the above

**Answer:** (a) Compilation error as "ZERO" is invalid pure specifier. Only 0 is preferred as pure specifier.

### 66. What is the output of the following piece of code? (L4)

```cpp
#include <iostream>
using namespace std;
class Base_class
{
public:
    void show()
    {
        cout << "Function Show in Base Class" << endl;
    }
};
class Derived_class : public Base_class
{
public:
    virtual void show() = 0;
};
class Derived_class_2 : public Derived_class
{
public:
    void show()
    {
        cout << "Function Show in derived Class_2" << endl;
    }
};
int main()
{
    Base_class obj1;
    Base_class *p;
    p = &obj1;
    p->show();
    Derived_class *p1;
    Derived_class_2 obj3;
    p1 = &obj3;
    p1->show();
    return 0;
}
```

- (a) Compilation error with usage of virtual in derived class
- (b) No error. No output
- (c) Function Show in Base Class  
  Function Show in derived Class_2
- (d) None of the above

**Answer:** (c) It is absolutely legal to use the keyword virtual with base class or derived class and it does not matter at all.

### 67. What is the output of the following piece of code? (L4)

```cpp
#include <iostream>
using namespace std;
class Base_class
{
public:
    void show()
    {
        cout << "Function Show in Base Class" << endl;
    }
};
class Derived_class : public Base_class
{
public:
    virtual void show();
};
class Derived_class_2 : public Derived_class
{
public:
    void show()
    {
        cout << "Function Show in derived Class_2" << endl;
    }
};
int main()
{
    Base_class obj1;
    Base_class *p;
    p = &obj1;
    p->show();
    Derived_class *p1;
    Derived_class_2 obj3;
    p1 = &obj3;
    p1->show();
    return 0;
}
```

- (a) Syntax error.
- (b) Compilation error.
- (c) Function Show in derived Class_2
- (d) Function Show in Base Class

**Answer:** (b) Compilation error. As the virtual function has been drafted wrongly. It could be either equated to 0 or { } should have been used.

### 68. What is wrong in the following code? (L4)

```cpp
#include <iostream>
using namespace std;
class Base_class
{
public:
    virtual void show() = 0;
};
class Derived_class : public Base_class
{
public:
    virtual void show()
    {
        cout << "\n" << "Test";
    }
};
int main()
{
    Base_class obj1;
    Base_class *p;
    p = &obj1;
    p->show();
    Derived_class obj2;
    p = &obj2;
    p->show();
    return 0;
}
```

- (a) Nothing wrong. The code will get compiled.
- (b) Syntax error.
- (c) No output.
- (d) Compilation error.

**Answer:** (d) Compilation error. Cannot declare variable 'obj1' to be of abstract type 'Base_class'. When a function is equated to 0, one cannot try to create an object for that class as it qualifies to be abstract class.

### 69. Which of the following are/is true about virtual function? (L3)

- (a) A virtual function gets qualified to be pure if assigned with 0.
- (b) Keyword pure is required to make a function pure virtual function.
- (c) If a pure virtual function is created in an abstract class, there will be a slot reserved for the function in the virtual table, with no address being stored there in the slot.
- (d) Instance of abstract class cannot be created.

**Answer:** (a), (c) and (d)

### 70. Which of the following is/are true about virtual function? (L3)

- (a) When a function gets called as virtual function, binding happens at compile time.
- (b) When a function gets called as virtual function, binding happens at runtime.
- (c) Assigning a NULL is equivalent to assigning 0 with respect to pure virtual function.
