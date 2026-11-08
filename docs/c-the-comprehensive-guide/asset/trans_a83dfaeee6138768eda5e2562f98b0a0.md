
```cpp
int main() {
    cout << length("Hipphopp") << "\n";  // const char* to string
    cout << twice(10).value_ << "\n";      // int to Value
    string name {"Gandalf"};
    cout << ( name + " the Grey") << "\n"; // string + const char*
}
```

**清单16.2** 当你调用一个函数，且该函数的参数导致编译器调用构造函数进行转换时，它会创建一个临时值。

length 函数接受一个 string 作为参数。然而，当我调用 length("Hipphopp") 时，我传递的是一个文本字面量，它是 `const char[]`。编译器会自动创建一个 string，仅仅是为了将其传递给 length()。在该语句之后，这个创建的 string 就会消失，因为它是一个临时值。

编译器使用的机制你已经知道了：自动类型转换。twice(10) 也会发生同样的情况。因为 Value 有一个带一个参数的构造函数，编译器可以利用它进行自动类型转换。瞧，10 是一个 int，而且匹配——于是创建了一个临时的 Value，在 twice 内部用作 v，最后被丢弃。

尤其是二元运算符喜欢创建临时值，比如加号 +。表达式 name + " the Grey" 是调用 operator+，参数类型为 string 和 const char*。该运算符将参数连接成一个新的 string，然后将其输出。连接后的结果就是临时值，在分号之后就不再需要了。

### 背景：左值、右值与合法窃取

在临时值的上下文中，你经常会在参考书和互联网上遇到诸如*lvalue*、*rvalue*和*rvalue 引用*等术语。这些并不是 C++ 带来的特性，而是用来描述 C++ 如何实现某些概念的技术术语。作为 rvalue 背后的概念，我觉得*temp-value*（临时值）这个术语更好。不过，在试图理解“如何”和“为什么”时，你经常会遇到这些技术术语。在下面的列表中，假设你已经声明了`int x, *p, a[10]`：

- **左值**  
  可以对其赋值的表达式，比如`x=1`、`*p=1`或`a[2]=1`。字母*l*来自 left（左），因为它们可以出现在赋值语句的左侧——即`lvalue = ...`。
- **右值**  
  不能对其赋值的表达式，比如`42=1`、`&x=1`或`x+1=1`。这些表达式只能出现在赋值语句的右侧——即`... = rvalue`。

> 这种区别很重要，因为右值只短暂存在（如果确实存在的话）——因此我用术语*temp-value*（临时值）来称呼它。临时值的内容可以被改变，而不会影响程序的其他任何部分。通常，人们会将资源从临时值转移到另一个对象，以节省一次复制。这对于理解移动操作非常重要，这将在16.9节中讨论。

## 16.3 析构函数与构造函数

如果你想检查对象何时被销毁，请在*析构函数*中完成。作为构造函数的对应物，它用于执行清理任务。这可能涉及清理类的数据字段或其他管理任务。

因为你目前只熟悉会自动去初始化的数据结构，所以这里将输出文本作为一项管理任务。给入门示例中的 MyValue 类注入一些实际内容。

```cpp
// https://godbolt.org/z/WPcTv37xKM
#include <string>
#include <iostream>
#include <iomanip>    // setw
using std::cout; using std::setw; using std::string;
struct MyValue {
    static int counter;          // static: exists only once for all instances
    int number_;                  // indentation level of this instance for output
    string name_;                 // name of this instance for output
    explicit MyValue(string name)
        : number_{++counter}     // increment indentation level per instance
        , name_{name}             // remember the object's name for output
    {
        cout << setw(number_) << " " << "Constructor " << name_ << "\n"; // output instance name
    }
    ~MyValue() {                  // destructor
        cout << setw(number_) << " " << "Destructor " << name_ << "\n";
    }
};
int MyValue::counter = 0;        // initialization of the static class variable
```

**清单16.3** 当一个对象被移除时，析构函数会被执行。

如此装备之后，你就可以像平常一样使用该对象了。为此，请在清单16.1中使用这种修改后的 MyValue 类型的具体变量。

```cpp
// https://godbolt.org/z/enneOWpzb
void function(const MyValue &valueParamRef) {
    MyValue localValue{"local"};
}

int main() {
    MyValue mvalue1{"mvalue1"};
    function( MyValue{"temp"} );
    function( mvalue1 );
    {
        MyValue mvalue2{"mvalue2"};
    }
}
```

**清单16.4** 这里创建和销毁了许多对象。

因此，你会得到下面清单所示的输出。

```text
Constructor mvalue1
  Constructor temp
    Constructor local
    Destructor local
  Destructor temp
    Constructor local
    Destructor local
    Constructor mvalue2
    Destructor mvalue2
Destructor mvalue1
```

**清单16.5** 该输出展示了对象何时被创建和销毁。

在 main 中，首先创建 mvalue1。你使用 setw 确保 MyValue 的第一个实例缩进深度为1，并通过++counter，所有后续实例缩进一个层级。计数器值同时被复制到 number_ 数据字段中。这样，你就可以在析构函数中使用与构造函数相同的缩进层级。你可以清楚地看到，mvalue1 也是最后一个被清理的对象：Destructor mvalue1 的输出发生在析构函数中。

你还会看到，为函数调用创建了 temp。在函数内部，local 被创建并再次移除——针对每次对 function 的调用都是如此。从函数返回后，temp 被移除——在语句结束时——而 mvalue1 仍然保留。

接下来，创建 mvalue2。然而，内部块的末尾立即到达，因此其析构函数紧接着被调用。直到这时，才到达 main 的末尾，从而也到达 mvalue1 有效期的末尾。

### 16.3.1 不需要析构函数

通常，没有必要在析构函数中做任何事，因为类的每个数据字段反正都会被清理。所以，如果你什么都不做，让析构函数为空，或者完全省略它，所有数据字段仍然会被移除。

只要使用我们目前已经覆盖的机制，你就不需要析构函数来清理。像`int`和`double`这样的基本数据类型，以及像`string`、`vector`和`fstream`这样的标准库类型，都会自动管理一切。

### 16.3.2 析构函数中的资源

但有些资源不会自动移除。原始指针和许多 C 数据类型必须在析构函数中处理。或者，你可以将整个内容包装在`shared_ptr`中，并使用*自定义删除器*。你将在第20章中了解更多相关信息。

假设你正在处理一个通过库提供给您的数据库，并提供相关的头文件作为编程接口。简化后，头文件可能看起来像下面这个清单。

```cpp
// https://godbolt.org/z/54dzsb31z
#ifndef DATABASE_HPP
#define DATABASE_HPP

typedef void* db_handle_t;

db_handle_t db_open(const char* filename);
void db_close(db_handle_t db);
int db_execute(db_handle_t db, const char* query);

#endif
```

**清单16.6** 一个资源 C 接口的简单示例。

因此，很明显，对于每个`db_open()`，你也必须调用一次`db_close()`。如果不这样做，可能发生各种情况：对数据库的写入可能被忽略，程序可能会泄漏数据库连接，最终无法再执行更多的`db_open()`，或者程序可能会崩溃。

为了确保每个`db_open()`都有一个`db_close()`被调用，请向编译器寻求帮助：构造函数调用和析构函数调用总是成对的。将资源包装在一个*资源包装器*中。

```cpp
// https://godbolt.org/z/6399qK9Ts
#include <iostream>                 // cout
#include "database.hpp"             // include the foreign API
```

