

![](img/6ba99460b0feb3585671a4612ff5fabb_560_0.png)

编译器确实会创建两个独立的类，一个名为 `PriceController<FredMaxPrice>`，另一个名为 `PriceController<JulieMaxPrice>`。它们彼此分离的程度，就如同你输入了两个独立的类，一个名为 `PriceControllerFredMaxPrice`，另一个名为 `PriceControllerJulieMaxPrice`。它们不是同一个类的不同实例——它们是不同的类。

到目前为止，在本节中，我们已经向你展示了可以把类型用作模板参数，或把某个特定类型的值用作模板参数。你也可以把类用作模板参数。下面的列表描述了每种参数类型：

- **值参数：**（ANSI 标准称这些为*非类型参数*，但我们更喜欢*值*这个叫法。）你可以在参数中为值给出类型和名称，如 `template <int MaxPrice>`。但出于某种原因，ANSI 标准禁止你在这里使用浮点值，如 `template <float MaxPrice>`，或使用类，如 `template <MyClass inst>`，或使用 void 类型，如 `template <void nothing>`。但你可以自由使用*指针*，所以 `template <float *MaxPrice>` 是允许的，`template <MyClass *inst>` 和 `template <void *MaxPrice>` 也是允许的。（不过，一般来说，你应该避免 `void *`，因为它不太有用；尽量让你的指针更具体，如 `int *MaxPrice`。）

- **typename 参数：** 你可以把类型用作类的参数，如 `template <typename T>`。然后，当你要求编译器基于该模板创建类时，你使用一个类型。并且当你使用 typename 时，必须确保你在类内部确实把它当作类型使用；不要只为参数传入一个变量。

- **类参数：** 记住，类本身就是一个类型，所以当你的模板需要一个类型时，你可以传入一个类名。但请记住，我们说的不是把类的实例传给模板；我们说的是通过在模板参数中指定类名来传入类本身。

![](img/6ba99460b0feb3585671a4612ff5fabb_560_1.png)

用于 Code::Blocks 的 GNU GCC 编译器会纠正其他编译器有时在你于模板内使用不允许的东西时给出的奇怪错误消息。问题在于，这些较旧的编译器不会为包含单词*模板*的那一行给出错误消息，例如 `template <float MaxPrice>`；相反，它们会为试图基于该模板创建类的那一行给出两条错误消息，例如 `PriceController<FredMaxPrice> FredsToaster;`。以下是我们看到的两条消息：

```
non-constant 'FredMaxPrice' cannot be used as template argument
ANSI C++ forbids declaration 'FredsToaster' with no type
```

## 清单 5-5：在模板中使用多个参数

```cpp
#include <iostream>

using namespace std;

template<typename K, typename V, int S>
class MyMap
{
protected:
    K key[S];
    V value[S];
    bool used[S];
    int Count;

    int Find(K akey)
    {
        int i;
        for (i=0; i<S; i++)
        {
            if (used[i] == false)
                continue;
            if (key[i] == akey)
            {
                return i;
            }
        }
        return -1;
    }

    int FindNextAvailable()
    {
        int i;
        for (i=0; i<S; i++)
        {
            if (used[i] == false)
                return i;
        }
        return -1;
    }

public:
    MyMap()
    {
        int i;
        for (i=0; i<S; i++)
        {
            used[i] = false;
        }
    }

    void Set(K akey, V avalue)
    {
        int i = Find(akey);
        if (i > -1)
        {
            value[i] = avalue;
        }
        else
        {
            i = FindNextAvailable();
            if (i > -1)
            {
                key[i] = akey;
                value[i] = avalue;
                used[i] = true;
            }
            else
                cout << "Sorry, full!" << endl;
        }
    }

    V Get(K akey)
    {
        int i = Find(akey);
        if (i == -1)
        {
            return 0;
        }
        else
        {
            return value[i];
        }
    }
};

int main()
{
    MyMap<char,int,10> mymap;

    mymap.Set('X',5);
    mymap.Set('O',6);
    mymap.Set('X',10);

    cout << mymap.Get('X') << endl;
    cout << mymap.Get('O') << endl;

    return 0;
}
```

运行此应用程序时，你将看到以下输出：

```
10
6
```

这个清单是一个很好的练习——不仅在你输入它时锻炼你的手指，而且有助于理解模板。注意模板定义的第一行：

```cpp
template<typename K, typename V, int S>
```

这个模板接受的不是一两个，而是（数一数！）三个参数。第一个是类型，我们将它用作 map 的键，所以称它为 K。第二个是类型，我们将它用作 map 的值，所以称它为 V。最后一个是 S，它不是类型。相反，S 是一个整数值；它表示 map 能容纳的键值对的最大数量。

后面的成员函数允许基于这个 `map` 的任何类的用户向 `map` 添加项，并从 `map` 中取回项。我们没有包含任何用于移除项的函数；你可能会思考可以怎样添加这样的功能。你甚至可以查看标准 C++ 库中 `map` 模板的头文件，看看该库的设计者是如何实现移除机制的。

## 对模板进行 typedef

如果你反复使用带有特定参数的某个模板，通常直接为它使用 `typedef` 是最简单的做法。例如，如果你有这样一个模板

```cpp
template <typename T>
class Cluck
{
public:
    T Chicken;
};
```

并且你发现自己反复使用 `Cluck<int>`，你可以对它进行 `typedef`，如下所示：

```cpp
typedef Cluck<int> CluckNum;
```

然后，任何时候你需要使用 `Cluck<int>`，都可以改用 `CluckNum`。这个 `main` 演示了 `CluckNum` 的用法：

```cpp
int main()
{
    CluckNum foghorn;
    foghorn.Chicken = 1;
    return 0;
}
```

![](img/6ba99460b0feb3585671a4612ff5fabb_564_0.png)

我们喜欢对模板使用 `typedef`，因为这样类名看起来就像普通的旧类名，而不是模板名。在前面的示例中，我们可以使用类名 `CluckNum`，而不是有点晦涩的 `Cluck<int>`。有趣的是，如果你作为程序员团队的一员工作，而其他程序员对模板的了解不如你多，那么如果你对模板进行 `typedef`，他们往往就不会那么畏惧。这样你就可以使用一个普通名称，而他们看到你的代码时也不会大脑过载。但别告诉他们这是我们说的。

![](img/6ba99460b0feb3585671a4612ff5fabb_564_1.png)

当编译器基于模板创建类时，人们说编译器正在*实例化*该模板。我们知道，大多数人使用*实例化*这个词来表示基于类创建对象。但如果你展开想象，就能看出模板本身也是一种类型，你可以从它创建其他类型。因此，基于模板的类实际上是*模板的实例*！而基于模板创建类的过程称为*模板实例化*。

![](img/6ba99460b0feb3585671a4612ff5fabb_565_0.png)

当你使用 typedef 为基于模板的特定类赋予更简单的名称时，编译器会基于该模板实例化这个类。或者换句话说，编译器会*实例化模板类*。

## 派生模板

如果仔细想想，你至少可以通过三种方式让类模板参与派生。你可以：

- 从类模板派生类
- 从类派生类模板
- 从类模板派生类模板

或者这三项你一项都不做。但如果你想了解它们，请阅读接下来的几节，我们会在其中展示它们如何工作。

### 从类模板派生类

你可以从模板派生一个类，并在这样做时指定该模板的参数。换句话说，如果这不算太绕弯子，可以这样想：你从一个模板创建一个类，再从那个创建出来的类派生你的最终类。

假设你有一个名为 `MediaHolder` 的模板，它的声明的前两行如下所示：

```cpp
template <typename T>
class MediaHolder
```

然后你可以从这个模板的一个特定情形派生一个类，如下面的类头文件所示：

```cpp
class BookHolder : public MediaHolder<Book>
```

这里我们创建了一个新类（基于 `MediaHolder`），名为 `MediaHolder<Book>`。然后从那个类派生了我们的最终类 `BookHolder`。清单 5-6 中展示的 `ClassFromTemplate` 示例是类 `MediaHolder` 的一个例子，该清单还包含一些好书和杂志，可以加入你的阅读清单。

