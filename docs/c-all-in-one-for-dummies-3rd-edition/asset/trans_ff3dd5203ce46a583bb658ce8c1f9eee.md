
我们不时会看到像这两行这样的代码。这样的代码并不容易理解，但一旦你知道这些行的含义，就能解读它们。

![](img/6ba99460b0feb3585671a4612ff5fabb_462_0.png)

我们倾向于直接使用 typedef，即使它就在相关函数之前。这样，其他人就能更清楚地知道该函数做什么。欢迎你照做。但如果你这样做，请确保你熟悉非 typedef 版本，这样当别人不使用 typedef 编写该版本时，你才能理解它是什么意思——或者当那个人对你说：“这个函数接受一个指向指针的指针的指针。”（是的，我们听人这么说过！）

### 函数指针

当应用程序运行时，应用程序中的函数存在于内存中；因此，就像内存中的其他任何东西一样，它们也有地址。拥有地址是件好事，因为这样人们就能找到你。

你可以通过取函数名并在函数名前加上取地址运算符（&）来获取函数的地址，如下所示：

```cpp
address = &MyFunction;
```

但要让这生效，你需要知道将 address 声明为什么类型。address 变量是一个指向函数的指针，而指定类型最干净的方式是使用 typedef（如 FunctionPointer01 示例所示）。（幸运的是，这是大多数人愿意使用 typedef 的少数情况之一。）

信不信由你，typedef 如下：

```cpp
typedef int (*FunctionPtr)(int);
```

这很难理解，但新类型的名称是 FunctionPtr。这定义了一个名为 FunctionPtr 的类型，它返回一个整数（最左边的 int），并接受一个整数作为参数（最右边的 int，必须放在括号中）。这条语句的中间部分是新类型的名称，你必须在它前面加一个星号，表示它是指向该表达式其余所有部分的指针。此外，你必须把类型名及其前面的星号放在括号内。

*第 IV 册 第 1 章 使用数组、指针和引用*

然后你就可以声明一些变量了！如下所示：

```cpp
FunctionPtr address = &MyFunction;
```

这一行将 `address` 声明为指向函数的指针，并将其初始化为 `MyFunction()`。现在，要让这生效，`MyFunction()` 的代码必须具有与 `typedef` 中声明的相同的原型。在这个例子中，它必须接受一个整数作为参数并返回一个整数。

因此，例如，你可能有一个像这样的函数：

```cpp
int TheSecretNumber(int x) {
    return x + 1;
}
```

然后你可以有一个 `main()`，它将该函数的地址存储在一个变量中——然后通过该变量调用该函数：

```cpp
int main(int argc, char *argv[])
{
    typedef int (*FunctionPtr)(int);
    int MyPasscode = 20;
    FunctionPtr address = &TheSecretNumber;
    cout << address(MyPasscode) << endl;
}
```

现在，为了让你可以说你见过它，下面是*不使用* `typedef` 时地址声明会是什么样子：

```cpp
int (*address)(int) = &TheSecretNumber;
```

判断线索应该是：你有两个并排放在括号中的东西，右边那组括号里只有类型。左边那组括号里有一个变量名。所以这一行不是声明类型；而是声明一个变量。

### 将变量指向成员函数

令人惊讶的是，大多数 C++ 程序员根本不知道存在一个名为 `this` 的指针。所以 `this` 是一个大秘密！尽情享受吧！秘密是什么？秘密就是你可以获取对象成员函数的地址，从而可以直接访问该成员函数实例的数据。哇哦！

现在请记住，类的每个实例都有自己的成员变量副本，除非这些变量是静态的。但函数在整个类中是共享的。是的，你可以区分静态函数和非静态函数。但这只是指它们访问哪些类型的变量：静态函数只能访问静态成员变量，而且你不需要通过实例来引用它们。非静态（也就是*普通*、*常规*）成员函数与特定实例一起工作。然而，在内存中，实际上只存在函数的一个副本。

那么成员函数如何知道要处理哪个实例呢？一个秘密参数会被传入成员函数：`this` 指针。假设你有一个名为 `Gobstopper` 的类，它有一个名为 `Chew()` 的成员函数。接下来，你有一个名为 `MyGum` 的实例，并像这样调用 `Chew()` 函数：

```cpp
MyGum.Chew();
```

当编译器为此生成汇编代码时，它实际上会向函数传入一个参数——`MyGum` 实例的地址，也就是 `this` 指针。因此代码中只有一个 `Chew()` 函数，但要调用它，你必须使用该类的特定实例。

因为内存中只有一个 `Chew()` 函数副本，所以你可以获取它的地址。但这样做需要某种看起来晦涩的代码。下面就是，简明扼要。假设你的类如下所示：

```cpp
class Gobstopper {
public:
    int WhichGobstopper;
    int Chew(string name) {
        cout << WhichGobstopper << endl;
        cout << name << endl;
        return WhichGobstopper;
    }
};
```

`Chew()` 函数接受一个字符串并返回一个整数。下面是指向 `Chew()` 函数的指针的 typedef：

```cpp
typedef int (Gobstopper::*GobMember)(string);
```

下面是一个 `GobMember` 类型的变量：

```cpp
GobMember func = &Gobstopper::Chew;
```

如果你仔细看这个 typedef，它看起来类似于普通函数指针。唯一的区别是类名和两个冒号位于星号之前。除此之外，它就是一个普通的旧式函数指针。

但是，普通函数指针仅限于指向具有特定参数类型集合和返回类型的函数，而这个函数指针共享这些限制，但还有一个进一步的限制：它只能指向 `Gobstopper` 类内的成员函数。

要调用存储在指针中的函数，你需要有一个特定的实例。注意，在前面代码中给 `func` 赋值时没有实例，只有类名和函数 `&Gobstopper::Chew`。所以要调用该函数，取一个实例，加上 func，然后调用！清单 1-2 中展示的 FunctionPointer02 示例包含一个完整示例，其中有类、成员函数地址和两个单独的实例。

### 清单 1-2：获取成员函数的地址

```cpp
#include <iostream>
#include <string>

using namespace std;

class Gobstopper
{
public:
    int WhichGobstopper;
    int Chew(string name) {
        cout << WhichGobstopper << endl;
        cout << name << endl;
        return WhichGobstopper;
    }
};

int main()
{
    typedef int (Gobstopper::*GobMember)(string);
    GobMember func = &Gobstopper::Chew;
    Gobstopper inst;
    inst.WhichGobstopper = 10;
    Gobstopper another;
    another.WhichGobstopper = 20;
    (inst.*func)("Greg W.");
    (another.*func)("Jennifer W.");
    return 0;
}
```

你可以在 main 中看到，首先我们为函数创建类型，称之为 `GobMember`，然后创建该类型的变量 `func`。接着我们创建 Gobstopper 类的两个实例，并给它们各自不同的 WhichGobstopper 值。

最后，我们调用成员函数，先为第一个实例调用，再为第二个实例调用。为了展示你可以获取带参数函数的地址，我们传入一个包含一些名字的字符串。

运行代码时，你可以从输出中看到，它确实为每个实例调用了正确的成员函数：

```text
10
Greg W.
20
Jennifer W.
```

现在，当我们说“为每个实例调用正确的成员函数”时，我们真正的意思是，代码每次调用的是同一个成员函数，但使用的是不同的实例。如果你从面向对象的角度思考，可以把每个实例看作拥有自己的成员函数副本。因此，说“为每个实例调用正确的成员函数”是可以的。

### 指向静态成员函数

在许多意义上，静态成员函数只是一个普通的旧式函数。区别在于，你必须使用类名来调用静态函数。但请记住，静态成员函数不与类的任何特定实例绑定；因此，调用静态函数时不需要指定实例。

下面是一个带有静态函数的示例类（如 FunctionPointer03 示例所示）：

```cpp
class Gobstopper
{
public:
    static string MyClassName() {
        return "Gobstopper!";
    }
    int WhichGobstopper;
    int Chew(string name) {
        cout << WhichGobstopper << endl;
        cout << name << endl;
        return WhichGobstopper;
    }
};
```

下面是一些代码，它获取静态函数的地址，并通过该地址调用它：

```cpp
typedef string (*StaticMember)();
StaticMember staticfunc = &Gobstopper::MyClassName;
cout << staticfunc() << endl;
```

注意，在最后一行中，我们不必引用特定实例来调用 staticfunc()——也不需要引用类。我们只是调用了它。因为事实是，在深处，静态函数只是一个普通的旧式函数。

### 关于引用

在本节中，我们会揭示使用引用的所有来龙去脉、优点和缺点。我们还会告诉你一些关于它们的事情。

本节假设你已经知道在编写函数时如何按引用传递参数。（有关按引用传递参数的更多信息，请参阅第 I 册第 7 章。）但是你可以
