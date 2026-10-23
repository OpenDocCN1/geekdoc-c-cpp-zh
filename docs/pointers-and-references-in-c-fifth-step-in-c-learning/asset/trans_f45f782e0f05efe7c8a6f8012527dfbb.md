

```
This is the derived class.
This is the derived class.
```

正如你所见，即使我们使用指向基类的指针和引用，由于函数重写，派生类的函数也会被调用。

## 指向常量成员变量的指针

下面是一个演示 C++ 中指向常量成员变量的指针用法的示例程序：

```cpp
#include <iostream>

class MyClass {
public:
    int myVariable;

    MyClass(int value) : myVariable(value) {}
    int getVariable() const { return myVariable; }
};

int main() {
    MyClass obj(42);
    const MyClass* ptr = &obj;  // Pointer to a constant object

    std::cout << "Value of myVariable: " << ptr->getVariable() << std::endl;

    // Accessing the constant member variable through the pointer
    std::cout << "Accessing constant member variable: " << ptr->myVariable << std::endl;

    // Attempting to modify the constant member variable
    // ptr->myVariable = 10;  // This would result in a compilation error

    return 0;
}
```

在上面的程序中，我们有一个名为 MyClass 的类，其中包含一个成员变量 myVariable。getVariable() 函数返回 myVariable 的值，并声明为 const，以表示它不会修改对象。

在 main() 函数中，我们创建了 MyClass 的一个对象 obj 并用 42 初始化它。然后我们声明一个类型为 const MyClass* 的指针 ptr，即指向 MyClass 常量对象的指针。这意味着我们不能修改 ptr 所指向的对象。

要通过指针访问常量成员变量，我们使用箭头运算符 (->)。在程序中，ptr->myVariable 用于通过指针 ptr 访问 myVariable 的值。

常量的含义是它确保成员变量的值不能通过指向常量的指针进行修改。在示例中，如果取消注释行 ptr->myVariable = 10;，它将导致编译错误，因为你试图修改一个常量成员变量。

使用指向常量成员变量的指针允许你在无法修改它的情况下访问成员变量的值。当你想提供对类某些数据成员的只读访问，确保它们保持不变时，这很有用。

## 指向成员变量的常量指针

下面是一个演示 C++ 中指向成员变量的常量指针用法的示例程序：

```cpp
#include <iostream>

class MyClass {
public:
    int myVariable;
};

int main() {
    MyClass obj;
    obj.myVariable = 42;

    // Declare a constant pointer to a member variable
    const int MyClass::*ptr = &MyClass::myVariable;

    // Access member variable through the constant pointer
    int value = obj.*ptr;

    std::cout << "Value: " << value << std::endl;

    // Attempt to modify the member variable through the constant pointer (error)
    // obj.*ptr = 50;  // This line will cause a compilation error

    return 0;
}
```

在这个程序中，我们定义了一个名为 MyClass 的类，其中只有一个成员变量 myVariable。然后我们声明了 MyClass 的一个对象 obj 并将 myVariable 的值赋为 42。

接下来，我们使用语法 const int MyClass::*ptr 声明一个指向成员变量的常量指针。这里，ptr 是一个常量指针，只能指向类 MyClass 的整数成员变量。

要通过常量指针访问成员变量，我们使用语法 obj.*ptr，它解引用指针并给出 myVariable 的值。

然而，由于指针被声明为 const，任何通过常量指针修改成员变量的尝试，例如 obj.*ptr = 50，都会导致编译错误。这是因为指针的常量性意味着它所指向的成员变量不能被修改。

在此上下文中，常量性的含义是成员变量可以通过常量指针读取但不能修改。这在你想将对成员变量的访问限制为只读操作，同时仍允许通过指针进行间接访问时很有用。它有助于强制不可变性并防止在使用指针时意外修改变量。

```cpp
(obj.*ptr)();  // Call the constant member function through the pointer

// Trying to call a non-constant member function through the same pointer will result in a
compilation error

// ptr = &MyClass::nonConstFunc;  // Compilation error: assigning non-const member function to const
member function pointer

return 0;
}
```

在这个示例中，我们有一个类 MyClass，其中有两个成员函数：nonConstFunc() 和 constFunc()。constFunc() 使用 const 关键字声明为常量成员函数，表示它不会修改对象的状态。nonConstFunc() 是一个非常量成员函数。

在 main() 函数中，我们首先使用 typedef 定义类型 FuncPtr，它表示指向 MyClass 的常量成员函数的指针。然后我们声明一个类型为 FuncPtr 的变量 ptr 并将常量成员函数 constFunc() 的地址赋给它。

要通过指针访问和调用常量成员函数，我们使用 .* 运算符。在这种情况下，obj.*ptr 解引用指针并在 obj 对象上调用常量成员函数。

需要注意的是，指向常量成员函数的指针只能被赋予常量成员函数的地址。尝试将非常量成员函数的地址赋给类型为 FuncPtr 的指针将导致编译错误，确保你不能通过常量成员函数指针意外调用非常量成员函数。

在此上下文中，常量性的含义是常量成员函数只能访问类内的其他常量成员函数和变量，确保它不会修改对象的状态。这提供了调用常量成员函数不会改变对象的数据成员的保证，在不希望进行数据突变的情况下允许安全且可预测的使用。

## 指向成员函数的常量指针

下面是一个演示 C++ 中指向成员函数的常量指针用法的示例程序：

```cpp
#include <iostream>

class MyClass {
public:
    void func() {
        std::cout << "Regular member function." << std::endl;
    }

    void constFunc() const {
        std::cout << "Constant member function." << std::endl;
    }
};

int main() {
    typedef void (MyClass::*MemberFuncPtr)() const;

    MemberFuncPtr ptr = &MyClass::constFunc; // Declare and initialize a constant pointer to a member function

    MyClass obj;
    (obj.*ptr)(); // Access the member function through the constant pointer

    return 0;
}
```

在这个程序中，我们有一个名为 MyClass 的类，它有两个成员函数：func() 和 constFunc()。constFunc() 函数使用 const 关键字声明为常量成员函数，这意味着它承诺不会修改调用它的类对象状态。

要声明指向成员函数的常量指针，我们使用 typedef 关键字。在这种情况下，MemberFuncPtr 被定义为指向一个不带参数、返回 void 且使用 const 关键字声明为常量成员函数的成员函数的指针。

在 main() 函数中，我们创建了一个名为 obj 的 MyClass 实例。然后我们声明并初始化常量指针 ptr，使其指向 constFunc() 成员函数。要通过常量指针访问成员函数，我们使用指针到成员运算符 .* 并使用函数调用语法 (obj.*ptr)() 调用该函数。

指针的常量性的含义是它只能用于访问常量成员函数。它确保通过指针访问的成员函数不会修改调用它的对象状态。这在你想确保在调用特定成员函数时对象状态保持不变的情况下很有用。

如果你尝试将非常量成员函数赋给常量指针或尝试通过常量指针调用非常量成员函数，将会导致编译错误。这有助于强制 const 正确性并防止在使用指向成员函数的常量指针时意外修改对象。

注意：示例中显示的 typedef 方法是在 C++ 中声明指向成员函数指针的传统方式。

