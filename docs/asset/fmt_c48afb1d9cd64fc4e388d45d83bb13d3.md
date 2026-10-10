
为了简单起见，为了让你了解抛出和捕获异常的机制，我使用了基本类型来抛出异常。然而，在实际程序中，典型的选择是抛出类对象，正如我们之后看到的那样。

# noexcept 指定符

C++98 提供了指定函数是否可能抛出异常以及它们的类型是什么的能力，使用了这些异常规范：对于：

```cpp
void f() throw(int, double);
void g() throw(); // 它不会产生异常。
```

`f()` 创建 `int` 和 `double` 类型的异常，而 `g()` 则不会。

尽管这看起来是一个很有用的特性，但异常规范在实践中效果并不好，并在 C++11 中被弃用。让我们再多讨论一下看看为什么。原则上，异常规范还应该包含从嵌套函数调用中可能抛出的异常。在这个示例中，`f()` 告知读者它可能抛出 `int` 和 `double` 异常。然而，`f()` 可能会调用另一个函数，该函数又调用另一个函数，等等，这可能会产生异常。在这种情况下，必须添加它们的类型。如果你编写所有的函数，你就可以添加它们。但如果这些函数是由其他人实现的（例如库函数），你需要找到可能的异常，这可能非常困难或不可能，例如，没有指定异常。总之，在实践中，这个特性被发现存在问题，C++11 弃用了它，而 C++17 删除了它；它保留了 `throw()` 作为 `noexcept` 的弃用同义词，我们接下来看到。

# 724 C++ 简介

C++11 委员会认为指示一个函数不抛出异常是有用的，并为此目的引入了 `noexcept` 指定符。总来说，我们知道函数不抛出异常可以简化我们在调用它时所编写的代码，因为我们不需要添加代码来处理异常。它还可以让编译器执行某些优化。

```cpp
void f() noexcept; // 它不抛出异常。
```

关于语法，在类成员函数中，`noexcept` 关键字被添加在 `const` 之后、`final`、`override` 或 `=0` 指定符之前（如果是虚拟函数的话）。如果虚拟函数被声明为 `noexcept`，则派生类中的函数重写也必须是 `noexcept`。

注意，当你声明一个函数为 `noexcept` 时，它可能会故意或无意地抛出异常，或调用其他抛出异常的函数。例如，假设类定义如下：

```cpp
void f() noexcept
{
    vector<A> v(100000);
}
```

`vector` 的构造函数可能无法为 `v` 的所有元素找到内存并抛出异常，尽管该函数声明为 `noexcept`。

因此，在函数声明中存在 `noexcept` 只是向阅读代码的人以及编译器指示该函数不抛出异常。然而，它并不能阻止异常发生；如果抛出了异常，`catch` 块将处理它。如果没有被捕获，程序将终止。例如，我们：

```cpp
void f(int *p)
{
    if (*p == 10)
        throw *p;
}
```

（注：原文后续有多段重复的相同内容，已按要求不重复输出）

# 726 C++ 导论

当潜在的失败是正常情况下，使用传统的 `if-else` 条件检查返回值的方法可能完全足够了。当然，这由你来决定。你可以结合使用返回值和异常，没有一条规则适用于所有应用，这由你来决定。将代码的理解与维护结合起来，可能是最佳实践。

此外，每位程序员都可能考虑如何处理错误。例如，你可能认为某个错误非常严重，无法解决，并且没有理由抛出异常。因此，你决定显示诊断信息或将其写入文件，并调用一个函数（例如 `exit()`）来结束程序。当然，你可以决定这样做，而其他人可能决定抛出异常，并让上层来处理该错误。

在大型应用程序中，你很可能需要使用异常机制，例如如果你正在使用会抛出异常的库。通常情况下，在分为若干部分并由不同程序员小组独立实现的大型应用开发中，为了更好地控制和维护程序，对于发生在不同部分且无法在本地处理的严重错误，最灵活、可靠且有效的错误管理策略是异常，这样异常就可以被转发并在中心点（如 `main()`）进行处理。

## 带类型的异常

除了使用基本数据类型（如 `int`）创建异常外，异常也可以抛出一个对象。通常情况下，这是更常见的选择。这种选择的优势之一是我们可以使用对象来区分创建异常的不同类型问题。另一个优势是，对象可以包含识别导致异常原因所需的所有信息。例如，让我们修改第一个程序，让异常抛出对象：

```cpp
#include <iostream> // 示例 22.3
#include <string>
using std::cout;
using std::cin;
using std::string;
class Err_Rpt {
private:
    int code;
    string msg;
public:
    Err_Rpt() : code(0), msg("") {}
    Err_Rpt(int c, const char *m) : code(c), msg(m) {}
    void show() const { cout << "C:" << code << ' ' << msg; }
};
int check_pswd(const string& str);
int main() {
    string pswd;
    while (1) {
        try {
            cout << "Enter password: ";
            cin >> pswd;
            check_pswd(pswd);
            break;
        }
        catch(const Err_Rpt& err)
        {
            err.show();
        }
        catch(int code)
        {
            cout << "C:" << code << " Error: Password must contain one special character at least\n";
        }
        catch(...)
        {
            cout << "Error: Another exception\n";
        }
        cout << "Password " << pswd << " is accepted !!!\n";
        return 0;
    }
}
```

```cpp
int check_pswd(const string& str)
{
    bool found;
    int i, len;

    len = str.size();
    if(len < 6)
        throw Err_Rpt(5, "Error: Short length\n"); /* 创建一个类型为 Err_Rpt 类对象的异常。 */
    int dig = 0;
    found = false;
    for(i=0; i<len; i++)
    {
        if(str[i] >= '0' && str[i] <= '9')
            dig++;
        if(str[i] == '!' || str[i] == '$' || str[i] == '#')
            found = true;
    }
    if(dig < 3)
        throw Err_Rpt(10, "Error: Password must contain three digits at least\n");
    if(found == false)
        throw 20;
    return 0;
}
```

首先，我修改了代码，让用户输入有效的密码，`break` 语句终止循环并显示密码。由于最后一个 `catch` 块之后没有代码，因此 `continue` 语句是不必要的。`check_pswd()` 抛出了一个 `int` 类型的异常以及另外两个 `Err_Rpt` 对象的类型异常。每个对象都用指示错误类型的值进行了初始化。这些异常被相应的 `catch` 块捕获，该块通过调用传递的对象的 `show()` 方法来显示成员中包含的信息。

注意，我们可以不抛出 `int` 异常，而是抛出另一个 `Err_Rpt` 类型的异常。例如，我们可以写成 `throw Err_Rpt();`，此时传递的对象不包含任何信息。

# 728 C++ 导论

我只是向你们展示一个结合了基本类型和用户定义类型异常的示例。在可能会从不同库抛出异常的大型应用程序，选择自己的类型比基本类型（例如整数值）更安全，以避免某些库使用了相同异常的情况。

让我问你们，我们可以传递一个引用的对象并使用 `catch(Err_Rpt err)`，或者传递一个基本类型的引用并使用 `catch(int& code)` 吗？没问题。事实上，当抛出异常时，即使指定了引用，实际传递的是对象的拷贝。也应该如此，`Err_Rpt` 对象在 `check_pwd()` 结束后就不再存在了。特别是当抛出异常时，`try` 块被退出并超出作用域，如果它被复制到一个临时对象中，然后就会被销毁。在 `try` 块内部抛出局部对象没有问题。注意，在多级异常系统中，如果对象最终被捕获，它可能会被多次复制，但最好不要包含过多的信息。逻辑上的问题是，既然对象被复制了，为什么要使用引用呢？我将在下一节回答你们。

## 异常与继承

上一个问题的回答是，正如我们在第 20 章所知，基类的引用可以指向派生自它的类的对象。例如，在下面的程序中我们有三个异常类，它们通过继承相互相关：

```cpp
#include <iostream> // 示例 22.4
class Err {
public:
    virtual void show() const {std::cout << "Err1\n";}
};
class Err2 : public Err {
public:
    virtual void show() const override {std::cout << "Err2\n";}
};
class Err3 : public Err2 {
public:
    virtual void show() const override {std::cout << "Err3\n";}
};
void f();
int main() {
    try {
        f();
    } catch (const Err& err) {
        err.show();
    }
    return 0;
}
```

729 异常

```cpp
void f ()
{
    throw Err3();
}
```

由于 `catch` 块是基类的引用，它可以匹配派生类。由于 `show()` 是虚函数，它会执行派生类的版本。如果不使用引用，派生类部分将被切片（sliced）。

# 730 C++ 导论

注意，如果在基类中声明虚函数不抛出异常（`noexcept`），在派生类中也必须如此。相反，如果虚函数可以抛出异常，我们可以在派生类中声明它不会抛出。例如：

```cpp
class A
public:
    virtual void f() noexcept;
    virtual void g();
};

class B : public A
public:
    virtual void f() {}; // 错误。
    virtual void f() noexcept override {}; // 正确。
    virtual void g() noexcept override {}; // 正确。
};
```

如果 `main()` 都没有捕获异常，关于该错误的诊断信息将会丢失。因此，最安全的做法是使用引用。在我们的示例中，如果不使用引用，`show()` 将始终被调用，无论 `throw` 的类型如何。

## 异常转发

异常处理系统是多级的。也就是说，每一层都尽可能处理它能处理的问题并将其留给上层。因此，如果异常没有被当前函数捕获，异常将转发到它的调用函数，然后从那里到上层调用函数，一直到 `main()`，直到某处找到 `catch` 块。如果 `main()` 没有捕获异常，默认情况下会终止。这个过程被称为栈回溯（stack unwinding）。例如，看下面的代码：

```cpp
int main() {
f() {
    g() {
h() {
}
try {
    try {
        try {
            throw 20;
        }
        f();
        g();
        h();
    } catch (int) {
    } catch (double) {
    } catch (const char*) {
    }
}
}
```

`h()` 中的异常被传递给上层，并最终被 `main()` 的 `catch` 块捕获，该块可以处理整数类型的异常。与其 `throw 20`，不如我们抛出 `1.2`；这个异常将被 `f()` 的 `catch` 块捕获，而如果我们抛出 `"Test"`；它将被 `g()` 的 `catch` 块捕获。如果定义了 `A` 类且 `a` 是它的对象且我们抛出 `a`；这个异常将到达 `main()`，由于没有针对 `A` 类型的 `catch` 块就会终止。

这个示例还展示了 `throw` 机制的一个非常重要的方面。`return` 将程序的执行传输到函数调用后的第一条语句，而 `throw` 将执行一直传输到第一个可以捕获该异常的 `catch` 块。

## 重新抛出异常

当 catch 捕获到一个异常时，它可能无法处理该异常，或者决定由更高层来处理更好。在这种情况下，你可以重新抛出异常，使其被传递到与异常类型相关的更高层，以接管其处理。这就是我们刚刚编写的 `throw`，且不带任何参数。`throw` 必须在 catch 块内部，或者在从 catch 块调用的函数（直接或通过调用链间接调用）的函数中执行。否则，`throw` 会导致程序终止。重新抛出的异常是被捕获的原始异常。例如，在下面的程序中，`throw` 抛出的初始异常一直传递到最终处理该异常的 catch 块：

```cpp
#include <iostream> // Example 22.5
void f();
void g();

int main() {
    try
    {
        f();
    } catch (int a)
    {
        std::cout << "int exception is caught: " << a << std::endl;
    }
    return 0;
}

void f() {
    try
    {
        g();
    } catch(int indirect) /* 因为 catch 块没有使用参数，所以我没有使用参数名。 */
    {
        std::cout << "int exception is rethrown\n";
        // 重新抛出异常。
    }
    std::cout << "f() terminates\n"; /* 因为 throw 重新抛出了异常，这条语句将不会执行。 */
}

void g() {
    throw 10;
}
```

`g()` 抛出的 `int` 异常被 `f()` 中的 `catch` 块捕获。`f()` 重新抛出它，并在 `main()` 中被捕获。`throw` 的原始参数也传递给了 `main()`。因此，程序显示：

int exception is rethrown

int exception is caught: 10

# 732 C++ 简介

顺便说一下，这个程序也是嵌套 try 块的示例。我们在上一节中也看到，一个 try 块同它的 catch 块可以嵌套另一个 try 块内部。在这个例子中，外部块在 `main()` 中，而内部块在 `f()` 中。每个 try 块都与其自己的组 catch 块关联，处理在其内部抛出的异常。当异常从内部块抛出时，它将由它自己的 catch 块处理。如果没有块匹配该异常，它将由外部 try 块的 catch 块处理。如果我们在 `f()` 中将 catch 块中的类型从 `int` 改为 `double`，那么异常将传播到 `main()` 中的外部 try 块。在那里，类型为 `int` 的 catch 块将捕获该异常。

通常情况下，作为一种输出参数，如果我们更改异常参数的值，就可以将引用传递给 catch 块。例如，让我们改变 `f()` 的 catch 块：

```cpp
catch(int& b)
{
    b = 20;
    std::cout << "int exception is rethrown\n";
    throw; // 重新抛出异常。
}
```

现在，当异常被重新抛出时，传递给 `main()` 的值将是 20。

## 异常与内存管理

当执行 `throw` 语句时，为 `throw` 和捕获该异常的 `catch` 块之间路径上的所有自动变量保留的内存将从栈释放。如果自动变量是对象，则会调用它的析构函数。例如：

```cpp
#include <iostream> // Example 22.6
#include <cstdlib> // for the exit()

class A
{
private:
    int code;
public:
    A(int c) {code = c};
    ~A() {std::cout << "a" << code << " is destroyed\n";}
};

void f();
void g();

int main() {
    try
    {
        f();
    }
    catch(int)
    {
        std::cout << "int exception is caught\n";
        exit(EXIT_FAILURE); // 我只是使用了 exit() 来记住它。
    }
    std::cout << "Program terminates\n";
    return 0;
}
```
