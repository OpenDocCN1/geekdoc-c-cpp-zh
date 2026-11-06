
## 第四部分：第5章——使用模板创建类

```cpp
float AbsoluteValueFloat(float x)
{
    if (x >= 0)
        return x;
    else
        return -x;
}
```

如果这些函数的使用者需要取一个整数的绝对值，他或她会使用 AbsoluteValueInt() 函数。但若要取一个 float 的绝对值，他或她则会改用 AbsoluteValueFloat() 函数。那 double 呢？或者其他某种数值类型呢？

但是，与其为 double 单独写一个函数、再为其他每一种类型各写一个函数，我们建议使用模板，如下所示：

```cpp
template <typename T> T AbsoluteValue(T x)
{
    if (x >= 0)
        return x;
    else
        return -x;
}
```

现在你只需要一个函数版本，就能处理任何数值类型，包括 double。该函数的使用者实际上可以根据需要创建自己的函数版本。例如，要使用这个函数的整数版本，我们只需在调用函数时，把类型名 int 放在函数名后的尖括号内：

```cpp
int n = -3;
cout << AbsoluteValue<int>(n) << endl;
```

如果我们想把这个函数用于 float，只需这样做：

```cpp
float x = -4.5;
cout << AbsoluteValue<float>(x) << endl;
```

注意我们是如何声明函数模板本身的。函数模板与普通函数真正的区别在于头部：

```cpp
template <typename T> T AbsoluteValue(T x)
```

首先，我们写上单词 template。然后跟任意数量的可选空格，再跟一个左尖括号（也就是小于号）。在尖括号之后，我们写上单词 typename、一个右尖括号（也就是大于号），然后是一个标识符名称。大多数人喜欢使用名称 T（因为它是英文单词 *类型*（type）的首字母），所以我们也就这样做了，随大流嘛。然后，我们写上函数头的其余部分，单独来看，它像这样：

```cpp
T AbsoluteValue(T x)
```

记住，T 代表一种类型。因此，函数头的这一部分表示一个名为 AbsoluteValue 的函数，它接受 T 作为参数并返回 T。所以，如果我们用整数基于这个模板创建一个函数，该函数将接受一个整数作为参数并返回一个整数。记住，T 基本上是一个类型名的占位符。因此，当编译器遇到这样一行时：

```cpp
cout << AbsoluteValue<float>(x) << endl;
```

它就会基于模板创建一个函数，并在看到 T 的地方都替换为 float。

然而，如果你有两行使用相同类型，如下所示

```cpp
cout << AbsoluteValue<float>(x) << endl;
cout << AbsoluteValue<float>(10.0) << endl;
```

编译器只会为这两行创建一个函数。（而且这两行不必紧挨着。）

### 重载与函数模板

如果你真的想冒险一试，为你的应用程序创造灵活性，可以将重载与函数模板一起使用。记住，*重载函数* 意味着你为一个函数创建两个不同的版本。实际上，你所做的是创建两个独立的函数，它们具有不同的参数（也就是说，参数数量不同或参数类型不同），但它们共享同一个名称。

看看 `FunctionOverloadingAndTemplates` 示例中的这两个函数：

```cpp
int AbsoluteValue(int x)
{
    if (x >= 0)
        return x;
    else
        return -x;
}

float AbsoluteValue(float x)
{
    if (x >= 0)
        return x;
    else
        return -x;
}
```

这些函数是重载的一个例子。它们接受不同的类型作为参数。（一个接受 int，另一个接受 float。）当然，你可以把这些函数合并成一个模板：

```cpp
template <typename T> T AbsoluteValue(T x)
{
    if (x >= 0)
        return x;
    else
        return -x;
}
```

但这真的有什么不同吗？毕竟，无论是在重载函数之后，还是在函数模板之后，你都可以使用下面两行代码：

```cpp
cout << AbsoluteValue<int>(n) << endl;
cout << AbsoluteValue<float>(x) << endl;
```

（我们假设 n 是整数，x 是 float。）然而，模板是更好的选择。首先，如果你使用重载形式，然后尝试这样做，就会遇到问题：

```cpp
cout << AbsoluteValue(10.5) << endl;
```

我们都知道 10.5 是 float；因此，编译器应该只调用重载函数的 float 版本。然而，Code::Blocks 自带的 GNU GCC 编译器却给了我们这样的错误消息：

```text
error: call of overloaded ‘AbsoluteValue(double)’ is ambiguous
```

有歧义？但看！消息说的是 AbsoluteValue (double)！嗯……显然，GNU GCC 编译器认为我们的 10.5 是 double，而不是 float。而实际上，你可以把 double 传给接受 int 的函数，也可以传给接受 float 的函数。编译器只会把它转换为 int 或 float，需要哪个就转换成哪个。并且因为编译器认为 10.5 是 double，它便认为可以把它传给重载函数的任一版本。于是这就给你留下一个选择：你可以把它强制转换为 float，或者创建该函数的第三个重载版本，一个接受 double 的版本。

真糟糕。至少 Code::Blocks 给了你一些关于问题的线索，因为扩展错误信息是

```text
note: candidates are: int AbsoluteValue(int)
note:                 float AbsoluteValue(float)
```

创建模板更容易。这就引出了模板版本更好的第二个原因：如果你想要该函数处理一种新类型，不需要再写另一个函数版本。

但如果你想重载一个函数模板呢？这听起来有点吓人，但你可以做到。代码清单5-9中展示的 OverloadedFunctionTemplate 示例包含一个重载的函数模板。

### 代码清单5-9：重载函数模板提供更大的灵活性

```cpp
#include <iostream>

using namespace std;

template <typename T> T AbsoluteValue(T x)
{
    cout << "(using first)" << endl;
    if (x >= 0)
        return x;
    else
        return -x;
}

template <typename T> T AbsoluteValue(T *x)
{
    cout << "(using second)" << endl;
    if (*x >= 0)
        return *x;
    else
        return -(*x);
}

int main()
{
    int n = -3;
    cout << AbsoluteValue<int>(n) << endl;

    float *xptr = new float(-4.5);
    cout << AbsoluteValue<float>(xptr) << endl;
    cout << AbsoluteValue<float>(10.5) << endl;

    return 0;
}
```

当我们传入一个指针时（就像 main() 中对 AbsoluteValue() 的第二次调用那样），编译器会判断出它需要使用模板的第二个版本。而为了确认在应用程序执行期间究竟使用了哪个版本、在什么时候使用，我们在每个函数模板的开头加入了一行 cout。运行这段代码时，你会看到：

```text
(using first)
3
(using second)
4.5
(using first)
10.5
```

从中间两行可以看出，计算机确实调用了模板的第二个版本。

你可以使用一个小技巧让事情轻松一点。大多数编译器允许你在函数模板调用本身中省略尖括号里的类型。编译器足够聪明，会根据你传入函数调用的类型，判断出要从模板构建什么类型的函数！相当神奇。下面是一个示例 main()，你可以用它替换代码清单5-9中的 main()：

```cpp
int main()
{
    int n = -3;
    cout << AbsoluteValue(n) << endl;

    float *ptr = new float(-4.5);
    cout << AbsoluteValue(ptr) << endl;
    cout << AbsoluteValue(10.5) << endl;

    return 0;
}
```

在这段代码中，我们把 AbsoluteValue<int>(n) 替换成了 AbsoluteValue(n)。运行修改后的代码清单5-9时，你会看到与运行代码清单5-9相同的输出。

### 将成员函数模板化

当你为一个类编写模板时，可以把函数模板放进类模板中。对于那些熟悉早期某些 C++ 版本（当时对模板的支持极少）的人来说，这似乎有点令人震惊。但当那股电流般的震惊消退后，我们都会明白，把模板函数放进模板类中是可行的。你只需在类中声明一个函数模板，如下所示：

```cpp
class MyMath
{
public:
    string name;

    MyMath(string aname) : name(aname) {}

    template <typename T> void WriteAbsoluteValue(T x)
    {
        cout << "Hello " << name << endl;
        if (x >= 0)
```
