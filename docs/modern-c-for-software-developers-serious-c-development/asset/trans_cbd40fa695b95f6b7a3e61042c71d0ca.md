

```cpp
bool operator ==(const type_info &obj);
bool operator !==(const type_info &obj);
const char *name();
bool before(const type_info &obj);
```

重载的运算符 `==` 和 `!=` 允许对两个 `type_info` 对象进行类型比较。

成员函数 `name` 返回对象类型的名称。例如：

```cpp
#include <typeinfo>
```

```cpp
string obj_type_name = typeinfo(obj).name();
```

```cpp
// 一个使用 typeid 的简单示例
```

```cpp
#include <iostream>
#include <typeinfo>
using namespace std;
```

```cpp
class MyClass1 {
};
class MyClass2 {
};
```

```cpp
int main() {
    int i, j;
    float f;
    char *p;
    MyClass1 obj1, obj3;
    MyClass2 obj2;
```

```cpp
    cout << "The type of i is: " << typeid(i).name() << endl;
    cout << "The type of f is: " << typeid(f).name() << endl;
    cout << "The type of p is: " << typeid(p).name() << endl;
```

```cpp
    cout << "The type of obj1 is: " << typeid(obj1).name() << endl;
    cout << "The type of obj2 is: " << typeid(obj2).name() << "\n\n";
```

```cpp
    if(typeid(i) == typeid(j))
        cout << "The types of i and j are the same\n";
    if(typeid(i) != typeid(f))
        cout << "The types of i and f are not the same\n";
    if(typeid(obj1) != typeid(obj2))
        cout << "obj1 and obj2 are of differing types\n";
```

```cpp
    if(typeid(obj1) == typeid(obj3))
        cout << "obj1 and obj3 are the same type\n";

    return 0;
```

```cpp
// 输出
The type of i is: i
The type of f is: f*
The type of p is: char*
The type of obj1 is: myclass1
The type of obj2 is: myclass2
The types of i and j are the same
The types of i and f are not the same
obj1 and obj2 are of differing types
obj1 and obj3 are the same type
```

`typeid` 最重要的用例是当它的参数是一个多态基类的指针时。在这种情况下，它将自动返回指向的实际对象的类型，无论该对象是基类对象还是派生类对象。

因此，通过使用 `typeid` 可以在运行时确定由基类指针所指向的多态对象的实际类型。

```cpp
// 一个在多态类层次结构上使用 typeid 的示例
#include <iostream>
#include <typeinfo>
using namespace std;

// Mammal 是一个多态类
class Mammal
{
public:
    virtual bool lays_eggs() { return false; }
};

class Cat: public Mammal {
};

class Platypus: public Mammal {
public:
    bool lays_eggs() { return true; }
};

int main()
{
    Mammal *p, AnyMammal;
    Cat cat;
    Platypus platypus;
    p = &AnyMammal;

```

```cpp
    cout << "p is pointing to an object of type " << endl;
    cout << typeid(*p).name() << endl;
```

```cpp
    p = &cat;
    cout << "p is pointing to an object of type " << endl;
    cout << typeid(*p).name() << endl;
```

```cpp
    p = &platypus;
    cout << "p is pointing to an object of type " << endl;
    cout << typeid(*p).name() << endl;

    return 0;
}
```

# 输出
p p is pointing to an object of type Mammal
p p is pointing to an object of type Cat
p p is pointing to an object of type Platypus

由于基类是多态的，尽管 `p` 是一个基类类型的指针，它仍然指向实际对象。

当 `typeid` 应用于多态类的基类指针时，指向的对象的类型是实际对象的类型。当 `typeid` 应用于非多态类层次结构的指针时，将返回指针在声明时所指向的对象的类型。例如，注释掉 `Mammal` 类中 `lays_eggs` 函数之前的 `virtual` 关键字，然后编译并运行程序进行观察。

当被解引的指针为空时，`typeid` 将抛出 `bad_type` 异常。

# typeid 与引用

指向多态类层次结构对象的引用的工作方式与指针相同。当 `typeid` 应用于多态类对象的引用时，它将返回实际被引用的对象的类型，该对象可能是派生类对象。

```cpp
// 使用引用参数演示 typeid
#include <iostream>
#include <typeinfo>
using namespace std;

// Mammal 是一个多态类
class Mammal {
public:
    virtual bool lays_eggs() { return false; }
};
class Cat: public Mammal {
};
class Platypus: public Mammal {
public:
    bool lays_eggs() { return true; }
};

void MammalType(Mammal& obj) {
    cout << "obj is referencing an object of type " << endl;
    cout << typeid(obj).name() << endl;
}

int main() {
    Mammal AnyMammal;
    Cat cat;
    Platypus platypus;

    MammalType(AnyMammal);
    MammalType(cat);
    MammalType(platypus);
}

// 输出
obj is referencing an object of type Mammal
obj is referencing an object of type Cat
obj is referencing an object of type Platypus
```

# 将 typeid 应用于类模板

`typeid` 函数可以应用于类模板的实例。类模板实例对象的类型由实际用于实例化特化的类型参数决定。使用不同模板参数实例化的同一类模板的两个实例是不同的类型。

```cpp
// 在类模板中使用 typeid
#include <iostream>
#include <typeinfo>
using namespace std;

// Foo 类声明
template <class T>
class Foo
{
    T a;
public:
    Foo(T i) { a = i; }
};

int main() {
    Foo<int> object1(10);
    Foo<double> object2(9);
    Foo<char> object3(7);

    cout << "Type of object1 is: " << typeid(object1).name() << endl;
    cout << "Type of object2 is: " << typeid(object2).name() << endl;
    cout << "Type of object3 is: " << typeid(object3).name() << endl;

    return 0;
}
```

# C++ 转换运算符

类型转换改变变量类型。C++ 定义了五种转换运算符。第一个是传统的转换。剩余的是 `dynamic_cast`、`static_cast` 和 `reinterpret_cast`。

# dynamic_cast

`dynamic_cast` 安全地在继承体系中上下转换指针和引用。它的语法为：

```cpp
dynamic_cast< new-type > ( expression )
```

表达式周围括号是必要的。`new-type` 是多态类中的类。

如果转换成功，`dynamic_cast` 返回 `new-type` 类型的值。如果转换失败且 `new-type` 是指针类型，则返回一个空指针。如果转换失败且 `new-type` 是引用类型，则会抛出 `std::bad_cast` 异常。

查看以下程序：

```cpp
#include <iostream>
#include <string>
using namespace std;

class Base
{ protected:
    int m_value;
public:
    Base(int value) : m_value(value) {}
    virtual ~Base() {}
};

class Derived : public Base
{ protected:
string m_name;
public:
    Derived(int value, string name) : Base(value), m_name(name) {}
    const string& getName() const { return m_name; }
}

Base* getObject(bool bDerivedObject) {
    if (bDerivedObject)
        return new Derived(1, "Apple");
    else
        return new Base(2);
}

int main() {
    Base* bptr = getObject(true);
    try {
        Derived* dptr = dynamic_cast<Derived*>(bptr);
        if (dptr) {
            cout << dptr->getName() << endl;
        }
    } catch (const std::bad_cast& e) {
        cout << e.what() << endl;
    }
    delete bptr;
    return 0;
}
```

