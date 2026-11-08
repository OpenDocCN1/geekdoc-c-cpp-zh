
当然，在编写用于继承的类时，首先应避免成员名称重复。该问题的理想解决方案是重写你的类。如果你无法重写这些类——例如，基类来自某种库——那么你将不得不在 main() 中限定函数名。你可以修改 main() 中的输出语句，使代码能够工作：

```cpp
std::cout << "cornflakes volume is " << cornflakes.Carton::volume() << std::endl
          << "cornflakes weight is " << cornflakes.FoodContainer::getWeight()
          << std::endl;
```

经过这一修改，程序将能够编译和运行，并产生以下输出：

```text
Box(double, double, double) called.
Carton(double,double,double,double,string_view) called.
FoodContainer(string_view) called.
CerealPack constructor
cornflakes volume is 240
cornflakes weight is 6.48
CerealPack destructor
FoodContainer destructor
Carton destructor. Material = Chipboard
Box destructor
```

从输出中可以看出，这种麦片将为你的一天提供扎实的开端——单包重量超过六磅。你还可以看到，构造函数和析构函数的调用顺序与单继承情境中的模式相同：构造函数从最基类到最派生类沿层次结构向下执行，而析构函数按相反顺序执行。CerealPack 对象拥有来自其继承链两条分支的子对象，并且这些子对象的所有构造函数都参与了 CerealPack 对象的创建。

使 Ex14_07 编译通过的另一种方法是，向任一基类的引用添加强制转换（我们转换为引用而不是类类型本身，以避免创建新对象）：

```cpp
std::cout << "cornflakes volume is " << static_cast<Carton&>(cornflakes).volume()
          << std::endl
          << "cornflakes weight is " << static_cast<FoodContainer&>(cornflakes).getWeight()
          << std::endl;
```

按照这种方式实现的可运行版本位于代码下载中的 Ex14_07A。

然而，显然非常不方便的是，我们当前 CerealPack 类的用户总是必须使用这些笨拙的变通方法来消除 volume() 和 getWeight() 成员的歧义。幸运的是，即使不能重命名成员（无论出于何种原因），你也可以防止这种情况发生。using 关键字允许你一劳永逸地明确指定：CerealPack 的 volume 应始终使用 Carton 的 volume() 成员计算，而其 weight 应使用 FoodContainer 的 getWeight() 成员计算。于是 CerealPack 类的定义变成如下所示（见 Ex14_07B）：

```cpp
export class CerealPack : public Carton, public FoodContainer
{
public:
  // Constructor and destructor as before...
  using Carton::volume;
  using FoodContainer::getWeight;
};
```

在本章前面，你遇到过 using 关键字的类似用法，用于从基类继承构造函数。在这种情况下，你用它来挑选多重继承的成员函数需要从哪个基类继承。现在，CerealPack 的用户——或者更常见的说法，吃早餐的人——可以简单地写成这样：

```cpp
std::cout << "cornflakes volume is " << cornflakes.volume() << std::endl
          << "cornflakes weight is " << cornflakes.getWeight() << std::endl;
```

显然，当对于应使用哪个多重继承成员有明确答案时，最后一种选择是首选。如果你已经在类定义中消除了继承歧义，就可以让你的类的用户免于应对原本必定会出现的编译器错误的麻烦。

### 重复继承

前面的示例演示了当基类的成员名称重复时，歧义会如何产生。另一种歧义可能在多重继承中出现：派生对象包含某个基类子对象的多个版本。你不能将同一个类作为直接基类使用多次，但最终可能会重复一个间接基类。假设 Ex14_07 中的 Box 和 FoodContainer 类本身派生自一个名为 Common 的类。图 14-9 显示了所创建的类层次结构。

![](img/020c376b6cc4874983a4344f51a256de_535_0.png)

*图 14-9.* 派生类中重复的基类

CerealPack 类继承 FoodContainer 和 Carton 两个类的所有成员。Carton 类继承 Box 类的所有成员，而 Box 和 FoodContainer 两个类都继承 Common 类的成员。因此，如图 14-9 所示，Common 类在 CerealPack 类中重复。这对 CerealPack 类型对象的影响是：每个 CerealPack 对象都会有两个 Common 类型的子对象。这种重复继承所产生的复杂情况和歧义通常被称为*菱形问题*——得名于图 14-9 这类继承图的形状。

可以想象，你实际上可能希望允许 Common 类重复。在这种情况下，你必须限定对 Common 类成员的每一次引用，以便编译器能够判断在特定实例中你引用的是哪个继承成员。你可以使用 Carton 和 FoodContainer 类名作为限定符，因为这两个类各自包含一个唯一的 Common 类型子对象。当然，在创建 CerealPack 对象时若要调用 Common 类的构造函数，你也需要使用限定符来指定正在初始化的是两个基类对象中的哪一个。

不过，更常见的情况是，你希望防止基类重复，因此让我们看看如何做到这一点。

### 虚基类

为了避免基类重复，你必须向编译器指明该基类在派生类中只应出现一次。你可以通过使用 `virtual` 关键字将该类指定为*虚基类*来做到这一点。FoodContainer 类将定义如下：

```cpp
export class FoodContainer : public virtual Common
{
  ...
};
```

Box 类也将使用虚基类定义：

```cpp
export class Box : public virtual Common
{
  ...
};
```

现在，任何将 FoodContainer 和 Box 类用作直接或间接基类的类，都会像往常一样继承这些基类的其他成员，但只会继承 Common 类的一个实例。派生类 CerealPack 将只继承 Common 类的一个实例。由于 Common 的成员在 CerealPack 类中没有重复，因此在派生类中引用这些成员时无需限定成员名称。

### 在相关类类型之间转换

每个派生类对象内部都有一个基类对象等待“脱出”。从派生类型到其基类的转换始终合法且自动。下面是 Carton 对象的定义：

```cpp
Carton carton{40, 50, 60, "Corrugated fiberboard"};
```

我们已经看到这个对象可以通过两种方式转换为 Box 类型的基类对象。第一种是通过复制构造函数：

```cpp
Box box{carton};
```

第二种是复制赋值：

```cpp
Box box;
box = carton;
```

两者都会将 carton 对象转换为新的 Box 类型对象，并将其副本存储在 box 中。所使用的赋值运算符是 Box 类的默认赋值运算符。当然，只使用 carton 中 Box 子对象的那部分；Box 对象没有空间容纳 Carton 特有的成员变量。这种效应称为对象切片，可以这么说，Carton 对象特有的部分被切掉并丢弃。

> **警告** 对象切片通常是需要提防的，因为当你并不希望派生类对象的派生成员被切掉时，它可能发生。在下一章中，你将学习一种机制，它允许使用指向基类对象的指针或引用来工作，同时保留派生类的成员甚至行为。

只要没有歧义，沿类层次结构向上转换（即朝向基类）就是合法且自动的。当两个基类各自具有相同类型的子对象时，就可能产生歧义。例如，如果你使用包含两个 Common 子对象的 CerealPack 类定义（如上一节所见），并初始化一个 CerealPack 对象 cornflakes，那么下面的代码将有歧义：

```cpp
Common common{cornflakes};
```

编译器将无法确定 cornflakes 的转换应指向 Carton 的 Common 子对象，还是 FoodContainer 的 Common 子对象。这里的解决方案是将 cornflakes 转换为 Carton& 或 FoodContainer&。下面是一个示例：

```cpp
Common common{static_cast<Carton&>(cornflakes)};
```

你无法获得沿类层次结构向下（即朝向更专门的类）的对象自动转换。Box 对象不包含任何可能派生自 Box 的类类型的信息，因此这种转换没有合理的解释。

### 小结

在本章中，你学习了如何基于一个或多个现有类定义类，以及类继承如何决定派生类的组成。继承是面向对象编程的基本特征，并使多态成为可能（多态是下一章的主题）。本章需要掌握的重点包括以下内容：

- 一个类可以派生自一个或多个基类，在这种情况下，派生类继承其所有基类的成员。
- 单继承涉及从一个基类派生类。多重继承涉及从两个或更多基类派生类。
- 对派生类继承成员的访问由两个因素控制：成员在基类中的访问说明符，以及基类在派生类声明中的访问说明符。

