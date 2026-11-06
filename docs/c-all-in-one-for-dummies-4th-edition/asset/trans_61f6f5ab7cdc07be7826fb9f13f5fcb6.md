
异常处理程序是通用的，必须把它放在列表的最后。创建 catch 块列表时，始终按从最具体到最不具体的顺序排列。下面是一个示例：

```cpp
try {
    ProcessData();
    ProcessMore();
    cout << "No problems!" << endl;
} catch (string excep) {
    cout << "Found an error. Here's the message.";
    cout << endl;
    cout << excep;
    cout << endl;
} catch (int num) {
    cout << "Found a numerical error. Here it is.";
    cout << endl;
    cout << num;
    cout << endl;
} catch (...) {
    cout << "An unknown exception occurred." << endl;
}
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_587_0.png)

如果函数调用抛出了异常，而你没有针对它的异常处理程序（因为 catch 块不处理所抛出的异常类型，或者你没有任何 try...catch 块），应用程序就会停止。应用程序会在控制台打印以下消息，然后立即终止：

```cpp
abnormal program termination
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_587_1.png)

以下编程规则能让你的用户愉快地无需了解异常：

- 知道何时调用了可能抛出异常的函数。
- 当调用可能抛出异常的函数时，要包含异常处理程序。
- 异常抛出时有多*深*并不重要；总得在某个地方由*某人*捕获它。一个函数可能调用另一个函数，后者又调用另一个函数，后者再调用一个会抛出异常的函数。如果中间函数都没有异常处理程序，就在外层函数中放一个。

### 重新抛出异常

在 catch 块内，后面不带任何内容的 throw 语句只会重新抛出同一个异常。尽管这种做法可能显得有点复杂（确实可能如此），但你可能有一个函数，其中包含一个在低层处理对象的 try...catch 块。然而，该函数可能没有处理异常所需的资源或信息，因此它把异常重新抛给上层函数，上层函数可能具备所需的访问权限。调用函数可能有一个实际能够处理该异常的 `try...catch` 块。换句话说，你的代码可能类似于 `Exception02` 示例中的代码：

```cpp
#include <iostream>

using namespace std;

void Inner() {
    throw string("Error!");
}

void Outer() {
    try {
        Inner();
    } catch (string excep) {
        cout << "Outer caught an exception: ";
        cout << excep << endl;
        throw;
    }
}

int main()
{
    try {
        Outer();
    } catch (string excep) {
        cout << "main caught an exception: ";
        cout << excep << endl;
    }
    return 0;
}
```

在前面的代码中，`main()` 调用 `Outer()`。`Outer()` 又调用 `Inner()`。`Inner()` 抛出一个异常，`Outer()` 捕获了它。但 `main()` 也想捕获该异常。因此，`Outer()` 重新抛出该异常。为此，调用后面不带任何内容的 `throw`，如下所示：

```cpp
throw;
```

运行此应用程序时，你会看到以下输出。

```
Outer caught an exception: Error!
main caught an exception: Error!
```

### 使用标准类别

通常应尽可能使用标准异常类别。前面的示例展示了一种处理异常的方法，但使用标准类别意味着你可以获得额外功能，并且知道接收方会如何解释该异常。此外，使用类别有助于创建异常层次结构，以便先处理最详细的异常。基于这些思路，Exception03 示例展示了如何使用 invalid_argument 异常类别。必须使用 C++11 或更高版本才能使用此示例。

```cpp
#include <iostream>

using namespace std;

bool CheckInt(int value) {
    if (value > 5) {
        return true;
    } else {
        throw invalid_argument("Input too small!");
    }
    return false;
}

int main() {
    try {
        cout << (CheckInt(6) ? "OK" : "Not Right") << endl;
        cout << (CheckInt(5) ? "OK" : "Not Right") << endl;
    } catch(const invalid_argument& ex) {
        cerr << "Invalid Argument: " << ex.what() << endl;
    }
    return 0;
}
```

注意，你使用了与平常相同的技术，例如调用 throw 来抛出异常。不过，在这种情况下，你创建的是类型为 invalid_argument 的异常对象，它需要一个详细说明错误的输入字符串。

catch 块依赖 const invalid_argument 引用，这是传递异常信息最有效且最不易出错的方法。注意，你可以调用 what() 方法来获取错误信息。此示例还展示了如何使用 cerr 将异常信息输出到标准错误流。

**本章内容**

- 有效地使用多态
- 派生新类时调整成员访问权限
- 多重继承新类
- 使虚继承正确工作
- 将一个类或类型放入另一个类或类型中

## 第4章：高级类用法

类具有惊人的强大能力。你可以用类做很多事情。在本章中，你将了解可在类中使用的许多额外特性。但这些并不只是你可能偶尔想用的小附加功能。如果你遵循本章的说明，你会发现你对 C++ 中类的理解会大大提升，并且你会在整个编程过程中希望使用其中的许多主题。

本章还讨论派生新类和继承成员时出现的许多问题。讨论内容包括虚继承和多重继承，这些是人们经常搞错的主题。作为讨论的一部分，你将了解将一个类或类型放入其他类中的各种方式。

![](img/128ab511de4e7360e167e3b15cdd5dd0_590_0.png)

你不必手动输入本章的源代码。事实上，使用可下载的源代码要容易得多。你可以在可下载源代码的 `\CPP_AIO4\Book\Chapter04` 文件夹中找到本章的源代码。有关如何找到这些源文件的详细信息，请参阅引言。

### 正确地继承

没有继承，面向对象编程（OOP）几乎不可能实现。是的，你可以将工作划分为对象，但真正的威力来自继承。然而，使用继承时必须小心，否则真的会给自己带来麻烦。在接下来的几节中，你将了解使用继承的不同方式——以及如何把这一切理清楚。

### 多态化继承

*多态*是指将一个对象用作基类的实例。例如，如果你有一个类 `Creature`，并从中派生类 `Platypus`，就可以把类 `Platypus` 的实例当作类 `Creature` 的实例来对待。如果你有一个以指向 `Creature` 的指针为参数的函数，这个概念就很有用。你可以传入指向 `Platypus` 的指针。

然而，你不能更进一步。你不能使用指向 `Creature` 的指针的指针。（请记住，创建指向指针的指针时，第一个指针是第二个指针变量的地址。）因此，如果你有如下函数：

```cpp
void Feed1(Creature *c) {
    cout << "Feed me!" << endl;
}
```

你可以自由地传入 `Platypus` 对象的地址，如下所示：

```cpp
Platypus *plato = new Platypus;
Feed1(plato);
```

然而，对于接受指针变量地址的函数（注意参数中的两个星号），如下所示：

```cpp
void Feed2(Creature **c) {
    cout << "Feed me!" << endl;
}
```

你不能传入指向 `Platypus` 实例的指针的地址，如下例所示：

```cpp
Platypus *plato = new Platypus;
Feed2(&plato);
```

如果尝试编译这段代码，就会遇到编译器错误。
