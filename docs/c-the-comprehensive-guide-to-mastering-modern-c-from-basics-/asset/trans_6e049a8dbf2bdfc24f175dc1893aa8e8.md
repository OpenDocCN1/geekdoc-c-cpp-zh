

| Variable | x1 | x2 | x3 | x4 | x5 |
|---|---|---|---|---|---|---|
| paramRef | Yes | | | | |
| localValue | | | | | | | |
| mvalue1 | | Yes | Yes | Yes | Yes |
| mvalue2 | | | Yes | | | |
| mvalue3 | | | | | | | |
| mvalue4 | | | | | Yes |

**表 16.1** 哪些变量什么时候可以在 "function()" 中使用？

与有效性紧密相关的是对象何时被*创建*以及何时被*销毁*。每个变量的生命周期始于它的*定义*——也就是说，它被*初始化*的时候。对于类来说，你也可以说它们被*构造*了，因为调用了*构造函数*。

变量的生命周期结束于离开作用域。具体来说，在我们的示例中，这意味着：

- *globalValue* 变量在退出 main 时被销毁。
- *paramRef* 变量在退出 function 时被销毁。
- *localValue* 变量在退出 function 时被销毁。
- *mvalue1* 变量在退出 main 时被销毁。
- *mvalue2* 变量在退出内部块时被销毁。
- *mvalue3* 变量在退出内部块时被销毁。
- *mvalue4* 变量在退出 main 时被销毁。
- MyValue{} 变量在该行的 ; 处被销毁。

## 16.2 临时值：短生存值

带有临时值的行特别值得注意。通过 `MyValue{}`，你创建了类的实例，然后将其作为参数传递给函数。然而，该实例并没有获得变量名。相反，你创建了一个临时值（也称为 temp-value）。因此，该值在语句结束时就会消失——根据经验法则，在下一个分号处。

当你创建一个临时值时，它不是一个声明，而是一个表达式。因此，你可以直接使用它——例如，作为函数的参数。

还有其他生成临时值的方法。例如，自动转换可以导致这种情况，如下面的列表调用 `length()` 时所示。

```cpp
// https://cppdbbolt.org/z/eKIErervis5
#include <string>
#include <iostream>
using std::string;using std::cout;
struct Value {
    int value_;
    Value(int value) // 1参数构造函数 = 类型转换
    : value_{value}
};
size_t length(string arg) {
    return arg.size();
}
Value twice(Value v) {
    return Value{v.value*2};
}
```

```cpp
int main() {
    cout << length("Hippopp") << "\n"; // const char* to string
    cout << twice(10).value << "\n"; // int to Value
    string name = "Gandalf";
    cout << (name + " the Gray") << "\n"; // string + const char*
}
```

**列表 16.2** 当你调用一个函数时，如果参数需要编译器调用构造函数来执行转换，它会创建一个临时值。

`length` 函数接受一个字符串作为参数。然而，当我调用 `length("Hippopp")` 时，我传递的是一个文本字面量，它是一个 `const char[]`。编译器会自动创建一个字符串，用于传递给 `length()`。语句结束后，这个创建的字符串就消失了，因为它是一个临时值。

编译器使用的机制你已经熟悉了：同样的事情发生在 `twice(10)` 中。由于 `Value` 有一个带有一个参数的构造函数，编译器可以使用它来执行自动类型转换。你看，10 是一个 `int` 且匹配——于是创建了一个临时的 `Value`，作为双份 `v`，并在结束时丢弃。

二进制运算符特别喜欢创建临时值，例如加法 `+`。`name + " the Gray"` 表达式是调用参数类型为 `string` 和 `const char*` 的运算符 `+`。运算符将参数连接成一个新字符串，然后输出。连接后的结果就是临时值，在 `;` 之后就不再需要了。

## 背景：Lvalues、Rvalues 和合法窃取

在临时值的语境下，你经常会在参考书和网上遇到 lvalue、rvalue 和 rvalue 引用等术语。这些并不是 C++ 引入的特性，而是描述 C++ 如何实现某些概念的专业术语。作为 rvalue 背后的一个概念，我认为 temp-value 这个术语更好。尽管如此，在尝试理解其如何做以及为什么时，你经常会遇到这些技术术语。在下面的列表中，假设你声明了 `int x, *p, a[10]`：

- Lvalue
  你可以对其赋值某些值的表达式，例如 `x=1`、`*p=1` 或 `a[2]=1`。字母 `l` 来自左（left），因为它们可以出现在赋值的左侧——即 `lvalue = ...`

- Rvalue
  你不能对其赋值任何值的表达式，例如 `42=1`、`&x=1` 或 `x+1=1`。这些只能出现在赋值右侧的表达式——即 `... = rvalue`。

这种区别很重要，因为 rvalue 只短暂存在（如果存在的话）——这就是我使用 temp-value 的原因。临时值的内容可以被改变而不影响程序的任何其他部分。

## 16.3 析构函数

如果你想检查对象何时被销毁，请使用析构函数。

```cpp
// https://gdbbolt.org/z/eKIErervis5
#include <string>
#include <iostream>
#include <iomanip>
using std::string;using std::cout;
struct Value {
    static int counter;
    string name_;
    explicit Value(string name) : name_(name) {
        counter++;
        cout << "Constructor " << name_ << " at depth " << counter << "\n";
    }
    ~Value() {
        counter--;
        cout << "Destructor " << name_ << " at depth " << counter << "\n";
    }
};

int Value::counter = 0;

void function(const Value &paramRef) {
  Value localValue("local");
}

int main() {
  Value mvalue1("mvalue1");
  function(Value{"temp"});
  function(mvalue1) {
    Value mvalue2("mvalue2");
  }
}
```

**列表 16.3** 如果你想检查对象何时被销毁，请使用析构函数。

在 `main` 中，`mvalue1` 首先被创建。你使用 `setw` 确保第一个实例的深度为 1，通过 `++counter`，后续实例的深度都增加一层。这样，你在析构函数中的缩进级别与构造函数相同。你可以清楚地看到 `mvalue` 也是最后一个被清理的对象：析构函数输出 `Destructor mvalue`。

你还看到 `temp` 在函数调用时被创建。在函数内部，`local` 被创建并销毁——对于两次调用 `function` 都是如此。从函数返回后，`temp` 被移除——而 `mvalue` 仍然存在。接下来创建了 `mvalue2`。然而，立即到达内部块，这就是为什么它的析构函数紧接着被调用。只有在 `main` 结束后，`mvalue` 的有效性才结束。

**列表 16.4** 这里，许多对象被创建和销毁。

因此，你将得到如下所示的输出。

- Constructor mvalue1
- Constructor temp
- Constructor local
- Destructor local
- Destructor temp
- Constructor local
- Constructor mvalue2
- Destructor mvalue2
- Destructor mvalue1

**列表 16.5** 此输出显示了对象何时创建和销毁。

### 16.3.1 不需要析构函数

通常情况下，没有必要在析构函数中做操作，因为类的每个数据字段都会被清理。所以，即使你什么都不做、让析构函数为空或完全省略，所有数据字段仍然会被移除。

只需使用我们目前涵盖的机制，你不需要析构函数来进行清理。基本数据类型如 `int` 和 `double`，以及标准库类型如 `string`、`vector` 和 `fstream`，都会自动管理一切。

