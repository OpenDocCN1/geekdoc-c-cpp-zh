
```
class Critter        // class definition — defines a new type, Critter
{
public:
    int m_Hunger;      // data member
    void Greet();      // member function prototype
};

void Critter::Greet()   // member function definition
{
    cout << "Hi. I'm a critter. My hunger level is " << m_Hunger << ".\n";
}

int main()
{
    Critter crit1;
    Critter crit2;

    crit1.m_Hunger = 9;
    cout << "crit1's hunger level is " << crit1.m_Hunger << ".\n";

    crit2.m_Hunger = 3;
    cout << "crit2's hunger level is " << crit2.m_Hunger << ".\n";

    crit1.Greet();
    crit2.Greet();

    return 0;
}
```

## 定义类

要创建新类型，可以定义一个类——代码将数据成员和成员函数分组。从类中，可以创建具有各自数据成员副本并可访问所有成员函数的独立对象。类就像蓝图。就像蓝图定义了建筑物的结构一样，类定义了对象的结构。就像工头可以根据同一蓝图建造许多房屋一样，游戏程序员也可以根据同一类创建许多对象。一些实际代码将有助于巩固这一理论。我在 Simple Critter 程序中以以下方式开始类定义

```
class Critter        // class definition — defines a new type, Critter
```

## 上海市基础教育学龄人口最高峰值预测

预计未来本市基础教育学龄人口规模变化趋势

![](img/c7e8651578bccd573227f684823b8754_280_0.png)

2029年将达到峰值184.5万

出生人口变化

小学在校生规模变化

初高中在校生规模变化

据预测，受出生人口变化影响，本市2025—2035年基础教育学龄人口呈先升后降态势，峰值出现在2029年附近。

```cpp
void Critter::Greet()  // member function definition
{
    cout << "Hi. I'm a critter. My hunger level is " << m_Hunger << ".\n";
}
```

该定义看起来像你见过的任何其他函数定义，除了有一点——我用 Critter:: 作为前缀来命名函数。当你在类外部定义成员函数时，需要用类名和作用域解析运算符对其进行限定，以便编译器知道该定义属于该类。

在成员函数中，我将 m_Hunger 发送到 cout。这意味着 Greet() 会显示通过该函数被调用的特定对象的 m_Hunger 值。这仅仅意味着成员函数显示了 critter 的饥饿程度。你可以在任何成员函数中仅通过使用成员的名称来访问对象的数据成员和成员函数。

## 实例化对象

当你创建一个对象时，你从一个类实例化它。事实上，特定的对象被称为类的实例。在 main() 中，我实例化了 Critter 的两个实例。

```cpp
Critter crit1;
Critter crit2;
```

因此，我有两个 Critter 对象——crit1 和 crit2。

## 访问数据成员

是时候让这些 critter 开始工作了。接下来，我给我的第一个 critter 设置一个饥饿程度。

```cpp
crit1.m_Hunger = 9;
```

前面的代码将 9 分配给 crit1 的数据成员 m_Hunger。就像访问对象的可用成员函数时一样，你可以使用成员选择运算符来访问对象的可用数据成员。

为了证明赋值成功，我显示 critter 的饥饿程度。

```cpp
cout << "crit1's hunger level is " << crit1.m_Hunger << ".\n";
```

前面的代码显示了 crit1 的数据成员 m_Hunger，并正确显示为 9。就像为可用数据成员赋值时一样，你也可以通过成员选择运算符获取可用数据成员的值。

接下来，我展示同样的过程对另一个 Critter 对象也适用。

```cpp
crit2.m_Hunger = 3;
cout << "crit2's hunger level is " << crit2.m_Hunger << ".\n\n";
```

这次，我将 3 分配给 crit2 的数据成员 m_Hunger 并显示它。

因此，crit1 和 crit2 都是 Critter 的实例，但各自独立存在，各自具有自己的身份。此外，每个都有自己的 m_Hunger 数据成员，具有自己的值。

## 调用成员函数

接下来，我再次让 critter 发挥作用。我让第一个 critter 打个招呼。

```
crit1.Greet();
```

前面的代码调用了 crit1 的 Greet() 成员函数。该函数访问调用对象的 m_Hunger 数据成员以形成其显示的问候。由于 crit1 的 m_Hunger 数据成员为 9，函数显示的文本为：Hi. I'm a critter. My hunger level is 9.

最后，我让第二个 critter 发声。

```
crit2.Greet();
```

前面的代码调用了 crit2 的 Greet() 成员函数。该函数访问调用对象的 m_Hunger 数据成员以形成其显示的问候。由于 crit2 的 m_Hunger 数据成员为 3，函数显示的文本为：Hi. I'm a critter. My hunger level is 3.

## 使用构造函数

当你实例化对象时，通常希望进行一些初始化——通常是为数据成员赋值。幸运的是，一个类有一个特殊的成员函数，称为构造函数，每次实例化新对象时都会自动调用。这是一个很大的便利，因为你可以使用构造函数来执行新对象的初始化。

```
public:
    int m_Hunger;

    Critter(int hunger = 0);    // constructor prototype
    void Greet();
};

Critter::Critter(int hunger)    // constructor definition
{
    cout << "A new critter has been born!" << endl;
    m_Hunger = hunger;
}

void Critter::Greet()
{
    cout << "Hi. I'm a critter. My hunger level is " << m_Hunger << ".\n\n";
}

int main()
{
    Critter crit(7);
    crit.Greet();

    return 0;
}
```

## 声明和定义构造函数

我在 Critter 中用以下代码声明一个构造函数：

```
Critter(int hunger = 0);    // constructor prototype
```

正如声明所示，构造函数没有返回类型。它不能——为构造函数指定返回类型是非法的。此外，在命名构造函数时你没有灵活性。你必须给它与类本身相同的名称。

> 提示
> 
> 默认构造函数不需要参数。如果你没有定义默认构造函数，编译器会为你定义一个最小的构造函数，它只是调用类的任何数据成员的默认构造函数。如果你编写自己的构造函数，那么编译器不会为你提供默认构造函数。通常最好有一个默认构造函数，因此在必要时应确保自行提供。实现此目的的一种方法是为构造函数定义中的所有参数提供默认值。

通过使用 private:，我的意思是其后（直到另一个访问级别说明符）出现的任何数据成员或成员函数都将是私有的。这意味着只有 Critter 类中的代码可以直接访问它。由于我在该部分声明了 m_Hunger，这意味着只有 Critter 中的代码可以直接访问对象的 m_Hunger 数据成员。因此，我不能像在之前的程序中那样通过对象在 main() 中直接访问对象的 m_Hunger 数据成员。所以 main() 中的以下行，如果取消注释，将是非法的语句：

//cout << crit.m_Hunger; //Illegal, m_Hunger is private!

因为 m_Hunger 是私有的，我不能从不属于 Critter 类的代码中访问它。再次强调，只有属于 Critter 的代码可以直接访问数据成员。

我只向你展示了如何使数据成员私有，但你也可以使成员函数私有。此外，你可以重复访问修饰符。因此，如果你愿意，可以在一个类中有一个私有部分，后跟一个公共部分，再后跟另一个私有部分。最后，成员访问默认为私有。在你指定访问修饰符之前，声明的任何类成员都将是私有的。

## 定义访问器成员函数

访问器成员函数允许间接访问数据成员。因为 m_Hunger 是私有的，我编写了一个访问器成员函数 GetHunger() 来返回数据成员的值。（现在你可以忽略 const 关键字。）

```
int Critter::GetHunger() const
{
    return m_Hunger;
}
```

我用以下行在 main() 中使用该成员函数：

```
cout << "Calling GetHunger(): " << crit.GetHunger() << "\n\n";
```

在前面的代码中，crit.GetHunger() 只是返回 crit 的 m_Hunger 数据成员的值，为 5。
