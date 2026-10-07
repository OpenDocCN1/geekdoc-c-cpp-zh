

```cpp
class Square : public Shape {
public:
    Square() {
        cout << "Square default constructor " << endl;
        SetColor(0);
        SetSideCount(4);
    }
    Square(int c) {
        cout << "Square one arg constructor " << endl;
        SetColor(c);
        SetSideCount(4);
    }
};
int main() {
    Square s(10);
    s.display();
    return 0;
}
```

我们从 `Shape` 类派生了 `Square` 类，以展示编译器如何调用嵌入类的构造函数。

输出：
Shape default constructor
Set Color to 0
Set Side Count to 0
Square integer constructor
Set Color to 10
Set Sid Count to 4
Color = 10
Sides = 4

注意，程序的运行结果并不符合你的预期！它包含了两个 `Square`（派生）类的构造函数，这些构造函数初始化了 `Shape`（基类）类的颜色和边数据成员。但 `Square`（派生）类的构造函数再次初始化了这些数据成员。

这些数据成员是如何首次初始化的？记住，派生类的构造函数会执行基类的构造函数。因此，`Square`（派生）和 `Shape`（基类）类的构造函数都初始化了 `Shape` 的数据成员 `color` 和 `side`。

C++ 面向对象

为了纠正对初始化函数的额外调用，我们可以简单地在 `Square`（派生）类的构造函数声明中使用冒号列表（colon list）。通过指定正确的 `Shape`（基类）构造函数，`Square`（派生）构造函数允许 `Shape`（基类）构造函数执行初始化。

```cpp
// shape2.cpp

#include <iostream>

class Shape {
private:
    int color;
    int sideCount;
public:
    Shape() {
        cout << "Shape default constructor" << endl;
        SetColor(0);
        SetSideCount(0);
    }
    Shape(int c, int sc) {
        cout << "Shape 2 arg constructor" << endl;
        SetColor(c);
        SetSideCount(sc);
    }
    void display() {
        cout << "color = " << color << endl;
        cout << "sides = " << sideCount << endl;
    }
    void SetColor(int c) {
        cout << "set color to " << c << endl;
        color = c;
    }
    void SetSideCount(int sc) {
        cout << "set side count to " << sc << endl;
        sideCount = sc;
    }
};

class Square : public Shape {
public:
    Square() : Shape(0, 4) {
        cout << "Square default constructor" << endl;
    }
    Square(int c) : Shape(c, 4) {
        cout << "Square one arg constructor" << endl;
    }
};
```

```cpp
int main() {
  Square s(10);
  s.display();
  return 0;
}
```

我们只需要在 `Square`（派生）类的构造函数的冒列表中指定相应的 `Shape`（基类）构造函数。`Square`（派生）类现在指定了调用哪个 `Shape`（基类）构造函数。通过这种方式，`Square` 类允许 `Shape` 类构造函数初始化它的数据成员。

```
output:
Shape 2 arg constructor
Set Color to 10
Set Side Count to 4
Square one arg constructor
Color = 10
Sides = 4
```

# 基类与派生类的析构函数

如果基类有构造函数，派生类通常也会提供，并且必须调用基类构造函数来初始化基类中的任何数据成员。相反，析构函数不需要严格处理。只有当派生类拥有在对象离开作用域时需要删除的成员时，派生类才需要提供析构函数。

```cpp
// dtor.cpp

#include <iostream>
#include <string.h>

namespace std {
class Base {
private:
    char *buf;
public:
    Base(char *s) {
        buf = new char[strlen(s) + 1];
        strcpy(buf, s);
    }
    ~Base() {
        delete [] buf;
    }
    char *getStr() {
        return buf;
    }
};
```

注意，构造函数将字符串参数拷贝到堆上，并将分配内存地址赋值给 `buf`。当 `Base` 类型对象离开作用域时，析构函数会删除此内存块。考虑一个从 `Base` 派生的新类会发生什么：

```cpp
class Derived : public Base {
private:
    char *upper;
public:
    Derived(char *s) : Base(s) {
        upper = new char[strlen(s) + 1];
        strcpy(upper, toupper(s));
    }
    ~Derived() {
        delete [] upper;
    }
    char *getUpper() {
        return upper;
    }
};
```

```cpp
int main() {
    Derived d("Haley Laurel");

    cout << d.getStr() << endl;
    cout << d.getUpper() << endl;
    return 0;
}
```

output:
Haley Laurel
HALALY LAUREL

注意，`Derived` 构造函数调用了 `Base` 构造函数，后者拷贝了 `s` 所指向的字符串。当 `Base` 类型对象离开作用域时，析构函数会删除此内存块。

# 构造函数重载

使用现有实例初始化类会调用拷贝构造函数。记住，如果你没有写构造函数，编译器会自动提供一个。注意，即使你为派生类写了拷贝构造函数，编译器也不会自动调用基类的拷贝构造函数。
