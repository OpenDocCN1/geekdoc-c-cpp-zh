
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

- (a) virtual 关键字使用错误
- (b) 基类中的 Show 函数  
  派生类中的 Show 函数  
  派生类 Class_2 中的 Show 函数
- (c) 派生类中的 Show 函数  
  派生类 Class_2 中的 Show 函数
- (d) 以上都不是

**答案：** (b) virtual 一旦在基类中使用，就会在整个代码中有效。

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

- (a) 编译错误
- (b) 基类中的 Show() 不能为空
- (c) 派生类中的 Show 函数
- (d) 以上都不是

**答案：** (c) 派生类中的语句将被打印，因为基类中的函数被称为“纯虚函数”。派生类中的函数将在派生类中重新定义。

### 57. 以下代码片段的输出是什么？(L4)

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

### 58. 以下代码片段的输出是什么？

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

- (a) 编译错误
- (b) 无错误。无输出
- (c) 当基类函数为虚函数时，不在派生类中重写该函数是非法的
- (d) 以上都不是

**答案：** (b) 无错误且无输出，因为派生类中的函数内部没有任何内容。

### 59. 以下代码片段的输出是什么？(L4)

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

- (a) 编译错误
- (b) 无错误。无输出
- (c) 非法，因为函数不能在基类和派生类中都设为虚函数
- (d) 以上都不是

**答案：** (b) 无错误且无输出，在基类和派生类中将同一函数设为虚函数并无害处。

### 60. 以下代码片段的输出是什么？(L4)

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

- (a) 编译错误
- (b) 无错误。无输出
- (c) 这是纯虚函数的演示
- (d) 以上都不是

**答案：** (c) 这是纯虚函数的演示，因为基类虚函数被赋值为 0，并且已在派生类中被重写。

### 61. 以下代码片段的输出是什么？(L4)

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

- (a) 编译错误
- (b) 无错误。无输出
- (c) 这是纯虚函数的演示
- (d) 以上都不是

**答案：** (c) 这是纯虚函数的演示，因为基类虚函数被赋值为 0，并且已在派生类中被重写。

### 62. 以下代码片段的输出是什么？(L4)

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

- (a) 编译错误
- (b) 无错误。无输出
- (c) 这是纯虚函数的演示
- (d) 以上都不是

**答案：** (a) 编译错误，因为 NULL 是无效的纯虚说明符。纯虚说明符只推荐使用 0。

### 63. 以下代码片段的输出是什么？(L4)

```cpp
#include <iostream>
using namespace std;
class Base_class
{
public:
    virtual void show() = "ZERO";
```

- (a) 编译错误
- (b) 无错误。无输出
- (c) 这是纯虚函数的演示
- (d) 以上都不是

**答案：** (a) 编译错误，因为 "ZERO" 是无效的纯虚说明符。纯虚说明符只推荐使用 0。

### 66. 以下代码片段的输出是什么？(L4)

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

- (a) 编译错误，因为派生类中使用了 virtual
- (b) 无错误。无输出
- (c) 基类中的 Show 函数  
  派生类 Class_2 中的 Show 函数
- (d) 以上都不是

**答案：** (c) 在基类或派生类中使用关键字 virtual 完全合法，而且完全没有影响。

### 67. 以下代码片段的输出是什么？(L4)

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

- (a) 语法错误。
- (b) 编译错误。
- (c) 派生类 Class_2 中的 Show 函数
- (d) 基类中的 Show 函数

**答案：** (b) 编译错误。因为虚函数的写法有误。它要么应等于 0，要么应使用 { }。

### 68. 以下代码有什么问题？(L4)

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

- (a) 没有问题。代码将能够编译。
- (b) 语法错误。
- (c) 无输出。
- (d) 编译错误。

**答案：** (d) 编译错误。不能将变量 'obj1' 声明为抽象类型 'Base_class'。当函数被置为 0 时，不能尝试为该类创建对象，因为它属于抽象类。

### 69. 以下关于虚函数的说法哪项/哪些是正确的？(L3)

- (a) 虚函数如果被赋值为 0，就有资格成为纯虚函数。
- (b) 需要使用关键字 pure 才能使函数成为纯虚函数。
- (c) 如果在抽象类中创建纯虚函数，虚表中将为该函数保留一个槽位，但该槽位中不会存储地址。
- (d) 不能创建抽象类的实例。

**答案：** (a)、(c) 和 (d)

### 70. 以下关于虚函数的说法哪项/哪些是正确的？(L3)

- (a) 当函数作为虚函数被调用时，绑定发生在编译时。
- (b) 当函数作为虚函数被调用时，绑定发生在运行时。
- (c) 对于纯虚函数而言，赋值 NULL 等同于赋值 0。

