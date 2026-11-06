
## 第IV部分：第3章：构造函数、析构函数和异常

继续运行这个应用程序。你会看到以下文本输出：

```
Found an error. Here's the message.
Oops, I found some bad data!
All finished.
```

仔细观察这个应用程序做了什么。在`main()`中，有一个对`ProcessData()`的调用，我们将它放在一个`try`块中。因为该调用位于`try`块内，所以计算机会调用该函数；如果该函数抛出异常，应用程序会自动从函数中退出并进入`catch`块。`catch`块接收被抛出的对象作为参数，很像函数的参数。

但是，如果`ProcessData()`函数没有遇到任何问题，因此没有抛出异常，那么该函数将完成其工作，应用程序将继续执行函数调用之后的代码。在这种情况下，`try`块内还有一行代码。如果没有异常，那么在`ProcessData()`函数完成后，计算机会执行`ProcessData()`调用之后的`cout`行。

把异常处理程序看作捕获错误的一种方式：如果抛出了异常，你的应用程序可以通过包含`catch`块来捕获该错误。

`try`/`catch`块完成后，应用程序将运行其后的任何行，无论是否存在异常。因此，在所有情况下，代码清单3-4都会执行以下行

```
cout << "All finished." << endl;
```

现在，在代码清单中，注意我们的`ProcessData()`函数调用了`throw`，这意味着它生成一个异常。通常，你可能不会像这个函数那样无缘无故地让函数抛出异常（除非你想逗用户玩），但我们这样做只是为了演示异常如何工作。而且，这很有趣！

这个特定的`throw`看起来像这样：

```
throw new string("Oops, I found some bad data!");
```

我们创建一个新的string实例，然后抛出它。你可以创建任何类的实例，它可以是指针或直接实例，取决于你更喜欢使用指针还是引用（这是你的选择）。

现在看代码清单3-4中的`catch`块。注意它以下面的内容开始：

```
catch (string *excep)
```

因为我们在函数中抛出了一个指向string实例的指针，所以这里我们捕获一个指向string实例的指针。一切都必须匹配。

你可以有多个catch块。假设可能抛出不同类型的异常。例如，你可能有一个像这样的另一个函数：

```cpp
void ProcessMore()
{
    throw new int(10);
}
```

另一个函数抛出了指向string的指针，但这个函数抛出指向整数的指针。注意！很多东西被抛来抛去！

然后，当你调用这两个函数时，你的try/catch块可以像这样：

```cpp
try
{
    ProcessData();
    ProcessMore();
    cout << "No problems!" << endl;
}
catch (string *excep)
{
    cout << "Found an error. Here's the message.";
    cout << endl;
    cout << *excep;
    cout << endl;
}
catch (int *num)
{
    cout << "Found a numerical error. Here it is.";
    cout << endl;
    cout << *num;
    cout << endl;
}
cout << "All finished." << endl;
```

如果你将此代码和ProcessMore()函数添加到代码清单3-4中，如果你想看到此应用程序处理整数异常，你可能想注释掉ProcessData()函数中的throw行。这是因为一旦throw语句发生，try块中行的执行就会停止，控制权将转移到适当的catch块。哪个catch块获得此殊荣取决于被抛出对象的类型。

### 抛出直接实例

你可以抛出不是指针的直接实例。在你的throw行中，你会这样做：

catch语句捕获的是引用。通常你只能对变量有引用，而不能对值有引用！但这里能工作是因为在计算机内部，应用程序会创建一个临时变量，而你在catch块中引用的就是这个临时变量。所以一切正常。

### 捕获任何异常

如果你想编写一个能捕获任何异常的通用catch处理程序，并且你并不关心实际捕获被抛出的对象，你可以这样编写处理程序：

```cpp
try
{
    ProcessData();
    ProcessMore();
    cout << "No problems!" << endl;
}
catch (...)
{
    cout << "An unknown exception occurred." << endl;
}
```

也就是说，不是在catch头部放入实际上相当于函数参数的内容，而是只放三个点，称为省略号。

![](img/6ba99460b0feb3585671a4612ff5fabb_519_0.png)

有些文字处理软件（Microsoft Word就是其中之一）可以将键入的三个句点转换为单个省略号字符。不要将该字符粘贴到代码编辑器中，因为编译器不知道如何处理它。相反，请键入三个句点。

除了其他处理程序之外，你还可以将省略号用作通用异常捕获器。这是一个例子：

```cpp
try
{
    ProcessData();
    ProcessMore();
    cout << "No problems!" << endl;
}
catch (string excep)
{
    cout << "Found an error. Here's the message:";
    cout << endl;
    cout << excep;
    cout << endl;
}
catch (int num)
{
    cout << "Found a numerical error. Here it is.";
    cout << endl;
    cout << num;
    cout << endl;
}
```

```cpp
void Outer()
{
    try
    {
        Inner();
    }
    catch (string excep)
    {
        cout << "Outer caught an exception: ";
        cout << excep << endl;
        throw;
    }
}

int main()
{
    try
    {
        Outer();
    }
    catch (string excep)
    {
        cout << "Main caught an exception: ";
        cout << excep << endl;
    }

    return 0;
}
```

在前面的代码中，main()调用Outer()。Outer()又调用Inner()。Inner()抛出一个异常，Outer()捕获它。但main()也想捕获该异常。所以我们让Outer()重新抛出该异常。你通过在throw后面不加任何内容来实现，像这样：

```
throw;
```

当你运行此应用程序时，你会看到以下输出。

```
Outer caught an exception: Error!
Main caught an exception: Error!
```

## 第4章：高级类用法

### 本章内容

- 有效地使用多态
- 在派生新类时调整private、protected和public之间的成员访问权限
- 多重继承新类
- 使虚继承正确工作
- 保持你的友元关系清晰，尤其是在类中
- 将一个类或类型放入另一个类或类型中

类非常强大。你可以用它们做很多事情。在本章中，我们讨论你可以在类中使用的许多额外特性。但这些并不是你可能偶尔想使用的小额外功能。如果你遵循本章中的说明，你会发现你对C++中类的理解将大大改善，并且你会在整个编程过程中想要使用这里的许多主题。

我们还讨论在派生新类和继承成员时出现的许多问题。这个讨论包括虚继承和多重继承，这些是人们经常搞砸的话题。我们还描述了将类和类型放入其他类中的方法。

### 正确地继承

没有继承，面向对象编程几乎不可能。是的，你可以将工作划分为对象，但真正的力量来自继承。然而，使用继承时必须小心，否则你可能会把事情搞砸。在接下来的小节中，我们讨论使用继承的不同方式——以及如何保持一切清晰。

#### 多态化你的继承

多态是指将一个对象用作基类的实例。例如，如果你有一个类Creature，并从中派生类Platypus，你可以将类Platypus的实例当作类Creature的实例来对待。如果你有一个函数接受指向Creature的指针作为参数，这个概念就很有用。你可以传递指向Platypus的指针。
