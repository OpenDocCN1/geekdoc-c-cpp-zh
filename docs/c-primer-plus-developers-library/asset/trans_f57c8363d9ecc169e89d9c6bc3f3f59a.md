

```cpp
    cout << "bad index: " << bad.bi_val() << endl;
}
cout << "\nNext try block:\n";
try
{
    sales2[2] = 37.5;
    sales1[20] = 23345;
    cout << "End of try block 2.\n";
}
catch(LabeledSales::nbad_index & bad)
{
    cout << bad.what();
    cout << "Company: " << bad.label_val() << endl;
    cout << "bad index: " << bad.bi_val() << endl;
}
catch(Sales::bad_index & bad)
{
    cout << bad.what();
    cout << "bad index: " << bad.bi_val() << endl;
}
cout << "done\n";

return 0;
}
```

以下是程序清单15.14、15.15和15.16中程序的输出：

```text
First try block:
Year = 2011
1220 1100 1122 2212 1232 2334
2884 2393 3302 2922 3002 3544
Year = 2012
Label = Blogstar
12 11 22 21 32 34
28 29 33 29 32 35
Index error in LabeledSales object
Company: Blogstar
bad index: 12

Next try block:
Index error in Sales object
bad index: 20
done
```

## 当异常误入歧途

异常被抛出后，有两次机会引发问题。首先，如果它是在带有异常规范的函数中抛出的，那么它必须与规范列表中的某个类型匹配。（请记住，在继承层次结构中，类类型既匹配该类型的对象，也匹配由它派生出的类型的对象。）如果异常与规范不匹配，这个不匹配的异常就被标记为*意外异常*，并且默认情况下会导致程序中止。（尽管 C++11 弃用了异常规范，但它们仍保留在语言中，也存在于一些现有代码中。）如果异常通过了第一道关卡（或者因为函数没有异常规范而避开了它），那么它就必须被捕获。如果它没有被捕获——在没有包含它的 try 块或没有匹配的 catch 块时就可能发生——该异常就被标记为*未捕获异常*，并且默认情况下会导致程序中止。不过，你可以改变程序对意外异常和未捕获异常的响应方式。下面从未捕获异常开始，看看如何改变。

未捕获异常不会立即引发中止。相反，程序会先调用一个名为 `terminate()` 的函数。默认情况下，`terminate()` 会调用 `abort()` 函数。你可以通过*注册*一个让 `terminate()` 代替 `abort()` 调用的函数，来修改 `terminate()` 的行为。为此，你要调用 `set_terminate()` 函数。`set_terminate()` 和 `terminate()` 都在异常头文件中声明：

```cpp
typedef void (*terminate_handler)();
terminate_handler set_terminate(terminate_handler f) throw();  // C++98
terminate_handler set_terminate(terminate_handler f) noexcept; // C++11
void terminate();                 // C++98
void terminate() noexcept;        // C++11
```

这里的 typedef 使 `terminate_handler` 成为指向无参数且无返回值函数的指针的类型名。`set_terminate()` 函数接受一个无参数且返回类型为 void 的函数名（也就是它的地址）作为参数。它返回先前注册的函数的地址。如果你多次调用 `set_terminate()` 函数，`terminate()` 会调用最近一次调用 `set_terminate()` 所设置的函数。

来看一个例子。假设你希望未捕获异常导致程序打印一条说明该情况的消息，然后调用 `exit()` 函数，并提供一个退出状态值 5。首先，你要包含异常头文件。你可以用 using 指令或适当的 using 声明使其声明可用，也可以使用 `std::` 限定符：

```cpp
#include <exception>
using namespace std;
```

接下来，你设计一个执行这两个必需操作并具有正确原型的函数：

```cpp
void myQuit()
{
    cout << "Terminating due to uncaught exception\n";
    exit();
}
```

最后，在程序开始时，将这个函数指定为你选定的终止操作：

```cpp
set_terminate(myQuit);
```

现在，如果异常被抛出且未被捕获，程序会调用 `terminate()`，而 `terminate()` 会调用 `myQuit()`。

接下来，我们来看意外异常。通过为函数使用异常规范，你为用户提供了了解该捕获哪些异常的手段。也就是说，假设你有以下原型：

```cpp
double Argh(double, double) throw(out_of_bounds);
```

那么你可能会这样使用该函数：

```cpp
try {
    x = Argh(a, b);
}
catch(out_of_bounds & ex)
{
    ...
}
```

知道该捕获哪些异常是件好事；回想一下，未捕获异常默认会中止程序。

然而，事情还不止这些。原则上，异常规范应当包含被讨论的函数所调用的函数可能抛出的异常。例如，如果 `Argh()` 调用了一个可能抛出 `retort` 对象异常的 `Duh()` 函数，那么 `retort` 应当同时出现在 `Argh()` 的异常规范和 `Duh()` 的异常规范中。除非所有函数都由你自己编写并且你很小心，否则无法保证这会正确完成。例如，你可能使用一个较旧的商业库，其函数没有异常规范。这表明你应当更仔细地研究：如果函数抛出的异常不在其异常规范中，会发生什么。（这也表明整个异常规范机制可能难以驾驭，这正是 C++11 弃用它的部分原因。）

其行为与未捕获异常非常相似。如果出现意外异常，程序会调用 `unexpected()` 函数。（你没预料到 `unexpected()` 函数？没人会预料到 `unexpected()` 函数！）这个函数反过来会调用 `terminate()`，而 `terminate()` 默认调用 `abort()`。正如有一个修改 `terminate()` 行为的 `set_terminate()` 函数一样，也有一个修改 `unexpected()` 行为的 `set_unexpected()` 函数。这些新函数同样在异常头文件中声明：

```cpp
typedef void (*unexpected_handler)();
unexpected_handler set_unexpected(unexpected_handler f) throw();   // C++98
unexpected_handler set_unexpected(unexpected_handler f) noexcept; // C++11
void unexpected();        // C++98
void unexpected() noexcept; // C++0x
```

不过，你为 `set_unexpected()` 提供的函数，其行为比用于 `set_terminate()` 的函数受到更多约束。具体来说，`unexpected_handler` 函数有以下选择：

- 它可以通过调用 `terminate()`（默认行为）、`abort()` 或 `exit()` 来结束程序。
- 它可以抛出一个异常。

抛出异常的结果（这里的第二个选择）取决于替换后的 `unexpected_handler` 函数所抛出的异常，以及那个抛出意外类型的函数原来的异常规范：

- 如果新抛出的异常与原来的异常规范匹配，那么程序会从那里正常继续；也就是说，它会寻找一个与新抛出异常匹配的 catch 块。基本上，这种做法接近于把意外类型的异常替换为预期类型的异常。
- 如果新抛出的异常与原来的异常规范不匹配，并且该异常规范*不*包含 `std::bad_exception` 类型，程序会调用 `terminate()`。`bad_exception` 类型派生自 exception 类型，并在异常头文件中声明。
- 如果新抛出的异常与原来的异常规范不匹配，并且原来的异常规范*确实*包含 `std::bad_exception` 类型，那么这个不匹配的异常会被替换为 `std::bad_exception` 类型的异常。

简而言之，如果你想捕获所有异常，无论它们是预期的还是其他情况，都可以像下面这样做。首先，确保异常头文件的声明可用：

```cpp
#include <exception>
using namespace std;
```

接下来，你设计一个替换函数，把意外异常转换为 `bad_exception` 类型，并且具有正确的原型：

```cpp
void myUnexpected()
{
    throw std::bad_exception();  //or just throw;
}
```

仅使用不带异常的 `throw` 会导致重新抛出原来的异常。不过，如果异常规范包含该类型，那么这个异常将被替换为一个 `bad_exception` 对象。

