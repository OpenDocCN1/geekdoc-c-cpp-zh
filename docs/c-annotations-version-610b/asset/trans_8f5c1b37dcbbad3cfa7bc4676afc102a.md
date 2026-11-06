
这不起作用的原因之一是变量`d_sp`具有全局作用域（它是一个函数指针，而不是`String`内的函数指针），而成员函数`get`定义在`String`类中，因此具有类作用域。`d_sp`是`String`类的数据成员这一事实在这里无关紧要。根据`d_sp`的定义，它指向一个位于*类外部*的函数。

因此，要定义指向类成员（数据或函数，但通常是函数）的指针，指针的作用域必须指明类作用域。这样，指向成员`String::get`的指针定义如下：

```
char const *(String::*d_sp)() const;
```

因此，通过在`*d_sp`指针数据成员前加上`String::`，它被定义为类`String`上下文中的一个指针。根据其定义，它是*a pointer to a function in the class String, not expecting arguments, not modifying its object's data, and returning a pointer to constant characters*。

### 16.2 定义指向成员的指针

指向成员的指针通过在普通指针表示法前加上相应的类名和作用域解析运算符来定义。因此，在上一节中，我们使用了`char const * (String::*d_sp) () const`来表示`d_sp`

- 是一个指针（`*d_sp`）；
- 指向类`String`中的某个东西（`String::*d_sp`）；
- 是一个指向`const`函数的指针，返回`char const *`（`char const * (String::*d_sp) () const`）。

因此，匹配函数的原型如下：

```
char const *String::somefun() const;
```

也就是类`String`中任何返回`char const *`的`const`无参函数。

在定义指向成员的指针时，构造函数指针的标准过程仍然适用：

- 将完全限定的函数名（即函数头，包括函数的类名）放在括号中：

    ```
    char const * ( String::somefun ) () const
    ```

- 在函数名本身之前紧挨着放置一个指针（星号（`*`））字符：

    ```
    char const * ( String:: * somefun ) () const
    ```

- 用指针变量的名称替换函数名：

    ```
    char const * (String::*d_sp) () const
    ```

这里是另一个例子，定义指向数据成员的指针。假设类`String`包含一个`string d_text`成员。如何构造指向该成员的指针？我们再次遵循标准过程：

- 将完全限定的变量名放在括号中：

    ```
    std::string (String::d_text)
    ```

- 在变量名本身之前紧挨着放置一个指针（星号（`*`））字符：

    ```
    std::string (String::*d_text)
    ```

- 用指针变量的名称替换变量名：

    ```
    std::string (String::*tp)
    ```

在这种情况下，括号是多余的，可以省略：

```
string String::*tp
```

或者，一个非常简单的经验法则是

- 定义一个普通（即全局）指针变量，
- 一旦你指向类内部的某个东西，就在指针字符前加上类名。

例如，下面的指向全局函数的指针

```
char const * (*sp)() const;
```

在加上类作用域后，它变成了指向成员函数的指针：

```
char const * (String::*sp)() const;
```

没有什么强制我们在目标（`String`）类中定义指向成员的指针。指向成员的指针可以定义在目标类中（因此它们成为数据成员），也可以定义在另一个类中，或者作为局部变量或全局变量。在所有这些情况下，指向成员的指针变量可以被赋予它所指向的那种成员的地址。重要的是，指向成员的指针可以在不需要指针目标类对象存在的情况下进行初始化或赋值。

初始化或给这样的指针赋值仅仅表明该指针指向哪个成员。这可以被视为某种相对地址；相对于调用该函数所针对的对象。初始化或赋值指向成员的指针时不需要对象。虽然允许初始化或赋值指向成员的指针，但（当然）如果不指定正确类型的对象，就不可能调用这些成员。

下面的例子说明了指向成员的指针的初始化和赋值（为了说明目的，类`PointerDemo`的所有成员都定义为public）。在例子中，使用了`&`运算符来确定成员的地址。这些运算符以及类作用域都是必需的，即使在成员实现内部使用时也是如此：

```
#include <cstddef>

class PointerDemo
{
    public:
        size_t d_value;
        size_t get() const;
};

inline size_t PointerDemo::get() const
{
    return d_value;
}

int main()
{
                                        // initialization
    size_t (PointerDemo::*getPtr)() const = &PointerDemo::get;
    size_t PointerDemo::*valuePtr       = &PointerDemo::d_value;

    getPtr    = &PointerDemo::get;          // assignment
    valuePtr  = &PointerDemo::d_value;
}
```

这没有什么特别之处。与全局作用域指针的区别在于，我们现在将自身限制在`PointerDemo`类的作用域内。由于这种限制，所有指针定义和所有使用其地址的变量都必须具有`PointerDemo`类作用域。

指向成员的指针也可以用于虚成员函数。指向虚成员时不需要特殊的语法。指针的构造、初始化和赋值方式与指向非虚成员的方式完全相同。

### 16.3 使用指向成员的指针

使用指向成员的指针调用成员函数需要存在指针所指向成员所属类的对象。对于在全局作用域操作的指针，使用解引用运算符`*`。对于指向对象的指针，可以使用作用于指针的字段选择运算符（`->`）或作用于对象的字段选择运算符（`.`）来选择相应的成员。

要将指向成员的指针与对象结合使用，必须指定指向成员的字段选择运算符（`.*`）。要通过对象指针使用指向成员的指针，必须指定“通过对象指针的指向成员字段选择运算符”（`->*`）。这两个运算符结合了字段选择（`.`和`->`部分）以到达对象中的相应字段，以及解引用：使用解引用操作来到达指向成员的指针所指向的函数或变量。

使用上一节中的例子，让我们看看如何使用指向成员函数的指针和指向数据成员的指针：

```
#include <iostream>

class PointerDemo
{
    public:
        size_t d_value;
        size_t get() const;
};

inline size_t PointerDemo::get() const
{
    return d_value;
}

using namespace std;

int main()
{
    size_t (PointerDemo::*getPtr)() const = &PointerDemo::get;          // initialization
    size_t PointerDemo::*valuePtr       = &PointerDemo::d_value;

    PointerDemo object;                                      // (1) (see text)
    PointerDemo *ptr = &object;

    object.*valuePtr = 12345;                 // (2)
    cout << object.*valuePtr << '\n' <<
            object.d_value << '\n';

    ptr->*valuePtr = 54321;                     // (3)
    cout << object.d_value << '\n' <<
            (object.*getPtr()) << '\n' <<      // (4)
            (ptr->*getPtr()) << '\n';
}
```

我们注意到：

- 在(1)处，定义了一个`PointerDemo`对象和一个指向此类对象的指针。
- 在(2)处，我们指定一个对象（因此使用`.*`运算符）来访问`valuePtr`所指向的成员。该成员被赋予一个值。
- 在(3)处，同一个成员被赋予另一个值，但这次使用指向`PointerDemo`对象的指针。因此我们使用`->*`运算符。
- 在(4)处，再次使用`.*`和`->*`，这一次通过指向成员的指针调用函数。由于函数参数列表的优先级高于指向成员的字段选择运算符，因此后者*必须用括号保护*。

当类中的某个成员根据配置设置而行为不同时，指向成员的指针可以有效地使用。再次考虑来自[9.3](#)节的`Person`类。`Person`定义了保存人名、地址和电话号码的数据成员。假设我们要构建一个雇员的`Person`数据库。可以查询雇员数据库，但根据查询数据库的人员类型，会提供姓名、姓名和电话号码，或所有存储的关于该人员的信息。这意味着像`address`这样的成员函数在查询数据库的人不被允许查看该人员地址的情况下必须返回类似`<not available>`的内容，而在其他情况下返回实际地址。

打开雇员数据库时，指定一个反映想要进行查询的雇员状态的参数。状态可以反映其在组织中的职位，如BOARD、SUPERVISOR、SALESPERSON或CLERK。前两类被允许查看所有雇员信息，SALESPERSON被允许查看雇员的电话号码，而CLERK只被允许验证一个人是否确实是组织成员。

我们现在在数据库类中构造一个成员函数`personInfo(char const *name)`。该类的标准实现可以是：

```cpp
string PersonData::personInfo(char const *name)
{
    Person *p = lookup(name);   // see if ‘name’ exists

    if (!p)
        return "not found";

    switch (d_category)
    {
        case BOARD:
        case SUPERVISOR:
            return allInfo(p);
        case SALESPERSON:
            return noPhone(p);
        case CLERK:
            return nameOnly(p);
    }
}
```
