
你预期输出是 `go()` called on `Sub`，但实际上，输出是 `go()` called on `Super`。这是因为该变量是一个 `Super` 引用，并且省略了 `virtual` 关键字。当调用 `go()` 方法时，它只是执行了 `Super` 的 `go()` 方法。因为它不是虚的，所以不需要考虑派生类是否已经重写了它。

> `WARNING` 尝试重写非虚方法会隐藏基类的定义，并且仅在派生类的语文中生效。

## `virtual` 是如何实现的

为了理解如何避免方法隐藏，你需要了解更多关于 `virtual` 关键字实际作用的知识。在 C++ 编译一个类时，会创建一个二进制对象，其中包含了该类的所有方法。在非虚情况下，将控制转移到相应方法的代码是硬编码的，基于调用方法时的编译时类型。

如果方法被声明为虚方法，则通过一个名为 `vtable`（虚函数表，取自 `virtual`）的特殊内存区域来调用正确的实现。对于每个拥有一个或多个虚方法的类，都有一个 `vtable`，该类的每个对象都一个指向该 `vtable` 的指针。`vtable` 指针指向虚方法的实现。通过这种方式，当在对象上调用方法时，跟随指针进入 `vtable`，并根据对象的实际类型执行方法的相应版本。

为了更好地理解 `vtable` 如何使方法重写成为可能，参考以下 `Super` 和 `Sub` 类示例。

```cpp
class Super
{
  public:
    virtual void func1() {}
    virtual void func2() {}
    void nonVirtualFunc() {}
};
class Sub : public Super
{
  public:
    virtual void func2() override {}
    void nonVirtualFunc() {}
};
```

对于此示例，假设你有以下实例：

```cpp
Super mySuper;
Sub mySub;
```

图 9-11 显示了这两个实例的 `vtable` 高层视图如下。`mySuper` 对象包含一个指向其 `vtable` 的指针。这个 `vtable` 有两个条目，分别对应 `func1()` 和 `func2()`。这些条目指向 `Super::func1()` 和 `Super::func2()` 的实现。`mySub` 对象包含一个指向其 `vtable` 的指针。这个 `vtable` 有两个条目，分别对应 `func1()` 和 `func2()`。这些条目指向 `Super::func1()` 和 `Super::func2()` 的实现。

以下代码使用 `<typeinfo>` 根据对象的类型打印消息：

```cpp
#include <typeinfo>
void speak(const Animal& inAnimal) {
    if (typeid(inAnimal) == typeid(Dog)) {
        cout << "Woof!" << endl;
    } else if (typeid(inAnimal) == typeid(Bird)) {
        cout << "Chirp!" << endl;
    }
}
```

每当你看到这样的代码时，应该立即考虑将该功能重新实现为虚方法。在这种情况下，更好的实现是在 `Animal` 类中声明一个名为 `speak()` 的虚方法。`Dog` 将重写该方法以打印 "Woof!"，而 `Bird` 将重写该方法以打印 "Chirp!"。这种方法更符合面向对象编程，即将与对象相关的功能交给这些对象本身。

> 警告：`typeid` 运算符仅在类至少有一个虚方法时才能正常工作。在没有任何虚方法的类上使用 `dynamic_cast` 将导致编译器错误。

`typeid` 运算符的主要价值之一用于日志记录和调试。以下代码利用 `typeid` 进行日志记录。`logObject()` 函数接收一个“可日志（loggable）”对象作为参数。这种设计使得任何继承自 `Loggable` 类并支持名为 `logMessage()` 方法的对象都可以。这样，`Loggable` 就是一个混入类（mixin class）。

```cpp
#include <typeinfo>
void logObject(const Loggable& inLoggableObject) {
    logfile << typeid(inLoggableObject).name() << " ";
    logfile << inLoggableObject.logMessage() << endl;
}
```

`logObject()` 函数首先将对象的类名写入文件，然后是它的日志消息。这样，当你读取日志时，就可以看到哪个对象负责文件中的每一行。

> 注意：`typeid` 运算符的主要价值之一用于日志记录和调试。

## 非公共继承 (Non-public Inheritance)

在之前的示例中，我们所有的继承关系都是 `public` 的。你可能会问继承权限是否可以是 `private` 或 `protected`。将基类的继承权限设置为 `private` 意味着派生类的外部无法访问基类的公有成员，而设置为 `protected` 则意味着只有派生类及其派生类可以访问。

使用非公共继承通常用于实现“实现（im-a）”关系而不是“是（is-a）”关系。有些程序员使用这种技术来组合基类的功能，但不希望暴露基类的接口给客户端。

> 非公共继承并不罕见，因为大多数程序员并不熟悉它。

## 虚基类 (Virtual Base Classes)

在本章早期，你学习了歧义基类（ambiguous base classes），这种情况发生在多个父类具有共同的父类时，如图 9-12 所示。解决方案是确保共享父类没有自己的功能。C++ 提供了另一种机制来解决这个问题，即使你不希望共享基类拥有自己的功能。如果共享基类是虚基类，则不会产生歧义。以下代码为 `Animal` 类添加了 `sleep()` 方法，并修改 `Dog` 和 `Bird` 类，以虚基类的方式继承 `Animal`。带有 `virtual` 关键字，在 `DogBird` 对象上调用 `sleep()` 将产生歧义并导致编译器错误，因为 `DogBird` 将拥有两个 `Animal` 子类，一个来自 `Dog`，一个来自 `Bird`。然而，当 `Animal` 被虚继承时，`DogBird` 只有一个 `Animal` 子类，因此调用 `sleep()` 不会有歧义。

![](img/a5a77830a2588caaa564a7658d3af652_317_0.png)

```cpp
class Animal {
public:
    virtual ~Animal() = default;
    virtual void sleep() {}
};
class Dog : virtual Animal {
public:
    void bark() override {
        cout << "Woof!" << endl;
    }
};
class Bird : virtual Animal {
public:
    void chirp() override {
        cout << "Chirp!" << endl;
    }
};
class DogBird : public Dog, public Bird {
};
int main() {
    DogBird db;
    db.sleep(); // 不歧义
    db.bark();
    db.chirp();
    return 0;
}
```

## 修改引用

引用始终指向它初始化时的同一个变量；引用一旦创建，就无法更改。这条规则导致了一些令人困惑的语法。如果你在声明引用时将一个变量“赋值”给引用，那么该引用将指向该变量。然而，如果你在之后将一个变量赋值给引用，那么引用所改变的将是所赋值变量的值。引用本身不会更新为指向该变量。以下是一个代码示例：

```
int x = 3, y = 4;
int&xRef = x;
xRef = y; // 将 x 的值改为 4。并不会让 xRef 指向 y。
```

你可能会尝试在赋值 `y` 的时候通过取它的地址来绕过这一限制：

```cpp
int x = 3, y = 4;
int&xRef = x;
xRef = &y; // 无法编译
```

这段代码无法编译。`y` 的地址是一个指针，而 `xRef` 被声明为 `int` 的引用，而不是指向指针的引用。

有些程序员甚至更进一步，试图规避引用的预意语义。如果将一个引用赋值给另一个引用会怎样？难道这不会让第一个引用指向第二个引用所指向的变量吗？你可能会想尝试这段代码：

```cpp
int x = 3, z = 5;
int&xRef = x;
int&zRef = z;
zRef = xRef; // 的是值，而不是引用
```

最后一行并没有改变 `zRef`。相反，它将 `z` 的值设置为 3，因为 `xRef` 指向 `x`，而 `x` 是 3。

> 你不能在初始化后更改引用所指向的变量；你只能改变该变量的值。

## 指针的引用和引用指针

你可以创建任何类型的引用，包括指针类型。这里有一个指向 `int` 指针的引用示例：

```
int* intP;
int&ptrRef = intP;
ptrRef = new int;
*ptrRef = 5;
```

这种语法有点奇怪。你可能不习惯看到 `&` 紧挨在一起。然而，其语义是直观的：`ptrRef` 是 `intP` 的引用，而 `intP` 是指向 `int` 的指针。修改 `ptrRef` 会改变 `int`。对指针的引用很罕见，但偶尔可能有用，正如本章后面“引用参数”部分将讨论的那样。

注意，取引用的地址与取其所指向变量的地址得到相同的结果。例如：

```cpp
int x = 3;
int&xRef = x;
int*xPtr = &xRef; // 引用的地址是对应值的指针
*xPtr = 100;
```

这段代码通过取指向 `x` 的引用的地址，使 `xPtr` 指向 `x`。给 `*xPtr` 赋值 100 会将 `x` 的值改为 100。由于类型不匹配，比较 "xPtr == xRef" 将无法编译；因为 `xPtr` 是指向 int 的指针，而 `xRef` 是 int 的引用。比较 "xPtr == &xRef" 和 "*xPtr == &x" 都能无错误编译且为真。

最后，请注意你不能声明指向引用的引用，或者指向引用的指针。

## 引用数据成员

正如第 8 章所解释的，类的数据成员可以是引用。引用如果不指向另一个变量就无法存在。因此，你必须在构造函数的初始化列表中初始化引用数据成员，而不是在构造函数体内。以下是一个简单的示例：

```
class MyClass {
public:
    MyClass(int& ref) : mRef(ref) {}
private:
    int& mRef;
};
```

详情请参阅第 8 章。

## 引用参数

C++ 程序员不使用独立的引用变量或引用数据成员。引用最常见的用法是作为函数和方法的参数。记住，默认的参数传递语义是值传递：函数接收参数的副本。当这些参数被修改时，原始参数保持不变。引用允许你为传递给函数的参数指定按引用传递。当你使用引用参数时，函数接收的是函数参数的引用。如果这些引用被修改，更改将反映在原始参数变量上。例如，这里有一个简单的交换函数来交换两个 int 的值：

```cpp
void swap(int& first, int& second) {
    int temp = first;
    first = second;
    second = temp;
}
```

你可以这样调用它：

```cpp
int x = 5, y = 6;
swap(x, y);
```

当用参数 `x` 和 `y` 调用 `swap()` 时，第一个参数初始化为指向 `x`，第二个参数初始化为指向 `y`。当 `swap()` 修改 `first` 和 `second` 时，`x` 和 `y` 实际上被改变。

就像不能用常量初始化普通的引用变量一样，你不能将常量作为参数传递给按引用传递的函数：

```
swap(3, 4); // 无法编译
```

> 注意 使用右值引用，可以将常量作为参数传递给按引用传递的函数。右值引用在本章中讨论。

## 来自指针的引用

当你有一个指向某个对象的指针，并且需要将其传递给接收引用的函数或方法时，会出现一个常见的困境。在这种情况下，你可以通过解引用指针将指针转换为引用。例如，你可以这样调用 `swap()`：

```cpp
int x = 5, y = 6;
swap(*x, *y);
```

当用参数 `x` 和 `y` 调用 `swap()` 时，第一个参数初始化为指向 `x`，第二个参数初始化为指向 `y`。当 `swap()` 修改 `first` 和 `second` 时，`x` 和 `y` 实际上被改变。

## 按引用传递与按值传递

当你想要修改参数时，需要按引用传递。然而，这提供了两个额外好处：

- 1. 效率：大型对象和结构体的拷贝可能花费很长时间。
- 2. 正确性：并非所有对象都允许深拷贝。正如第 8 章解释的，如果你想利用这些优点但不想允许对象被修改，可以将参数标记为 `const`。该主题有详细介绍。

## 引用返回值

你也可以从函数或方法返回一个引用。这样做的主要原因是为了效率。为了避免拷贝整个对象，返回该对象的引用。当然，只有当该对象在函数结束后仍继续存在时，你才能使用这种技术。

> 不要从函数或方法返回局部作用域变量的引用，例如栈上自动分配的变量。

如果你要返回的类型支持移动（在本章稍后讨论），那么按值返回与返回引用一样高效。

返回引用的另一个原因是如果你希望直接将返回值作为左值（赋值语句的左侧）。多个重载运算符会返回引用。第 8 章展示了一些示例，你可以在第 14 章了解该技术的更多应用。

## 在引用和指针之间做选择

C++ 中的引用可能是多余的：几乎所有用引用能做的事情，都可以用指针完成。例如，你可以这样写之前所示的 `swap()` 函数：

```cpp
void swap(int* first, int* second)
{
    int temp = *first;
    *first = *second;
    *second = temp;
}
```

然而，这比使用引用的版本杂乱：引用让你的程序更简洁、更易理解。引用也比指针安全：不存在空引用，且你不需要显式解引用引用，因此不会遇到与指针相关的任何解引用错误。这些关于引用更安全的论点在没有任何指针的情况下才有效。例如，考虑以下这个接收 `int` 引用的函数：

```
void refcall(int& t) { ++t; }
```

你可以声明一个指针并将其初始化为内存中的某个随机位置。然后解引用该指针并将其作为引用参数传递给 `refcall()`，如下代码所示。这可以通过编译，但在执行时会崩溃。

```cpp
int* ptr = (int*)8;
refcall(*ptr);
```

大多数情况下，你可以使用引用代替指针。对对象的引用以与对象指针相同的方式支持多态。只有一种需要使用指针的情况是你需要更改它所指向的位置。请记住，你不能更改引用所引用的变量。例如，当动态分配内存时，你需要将结果的指针存储在指针中而不是引用中。第二个需要使用指针的用例是可选参数。例如，指针参数可以是可选的，并带有默认值 `nullptr`，这在引用参数中是无法实现的。

另一种区分在参数和返回类型中何时使用指针或引用的方法是取决于代码是否拥有该内存。如果接收代码变得负责释放与对象相关的内存，则它必须接收一个指向对象的指针，或者最好是一个智能指针，这是转移所有权的推荐方法。如果接收变量的代码不应该释放内存，则它应该接收引用。

> 注意：除非你需要更改引用所指向的内容，否则请使用引用代替指针。

考虑一个函数，它将一个 int 数组拆分为两个数组：一个偶数数组和一个奇数数组。该函数并不知道源数组中有多少个数字是偶数或奇数，因此它应该在检查源数组后动态为目标数组分配内存。它还应该返回两个新数组的大小。总而言，有四个项需要通过引用传递。C++ 的实现方法——显然，该函数看起来如下：

```cpp
void separateOddsEvens(const int arr[], int size, int** odds,
    int* numOdds, int** evens, int* numEvens) {
    // 统计奇数和偶数的数量
    *numOdds = 0; *numEvens = 0;
    for (int i = 0; i < size; i++) {
        if (arr[i] % 2) {
            (*numOdds);
        } else {
            (*numEvens);
        }
    }
    // 分配两个适当大小的数组
    *odds = new int[*numOdds];
    *evens = new int[*numEvens];
    // 将奇数和偶数拷贝到新数组中
    int oddsPos = 0, evensPos = 0;
    for (int i = 0; i < size; i++) {
        if (arr[i] % 2) {
            (*odds)[oddsPos++] = arr[i];
        } else {
            (*evens)[evensPos++] = arr[i];
        }
    }
}
```
