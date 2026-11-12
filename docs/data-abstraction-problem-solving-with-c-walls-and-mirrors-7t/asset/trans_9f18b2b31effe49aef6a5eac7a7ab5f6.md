

```
string secretName = "Rumpelstiltskin";
nameBox.setItem(secretName);
MagicWand elfWand;
wandBox.setItem(elfWand);
```

> 注意：通过使用模板，你可以定义一个涉及任何类型数据的类，甚至包括在你设计和实现类之后才创建的数据类型。

## C1.4 继承

既然 PlainBox 类已经编写完成，我们将来看另外两个盒子。玩具盒与我们的普通盒子非常相似，但它有一个额外的特性，即颜色，我们可以使用枚举类型 Color 来表示它。我们在创建玩具盒时设置其颜色。游戏中的角色可以询问盒子的颜色，但不能更改它。以下是这些方法的 UML 表示法：

- +getColor(): string
- +setItem(ItemType theItem)
- +getItem(): ItemType

setItem 和 getItem 方法的行为与为 PlainBox 类实现的同名方法完全相同。我们可以通过继承来复用 PlainBox 中的代码。继承允许我们复用和扩展已经完成和测试过的工作。

### C1.4.1 基类和派生类

我们可以将 PlainBox 用作 ToyBox 类的基类（或父类）。你可以把基类看作父类。ToyBox 类是 PlainBox 类的派生类（或子类）。要指示 ToyBox 从 PlainBox 派生，我们在 ToyBox 的类头中使用以下语法：

```
class ToyBox : public PlainBox<ItemType>
```

派生类的任何实例也被视为基类的实例，可以在程序中任何可以使用基类实例的地方使用。另外，当关键字 public 用于基类时，基类中公开定义的任何方法或数据字段都可以在派生类的实例中使用。在 C++ 中，派生类继承其基类的所有成员，除了构造函数和析构函数。也就是说，派生类除了它自己定义的成员外，还拥有基类的数据字段和方法，尽管它只能访问公开定义的成员。派生类还可以修改任何继承的公共方法。

如清单 C1-5 所示，如果不需要修改基类的任何方法，ToyBox 只定义其特有的构造函数和新方法。setItem 和 getItem 方法从 PlainBox 类继承，可以在我们的 ToyBox 类中使用。

| 清单 C1-5 类 ToyBox 的模板头文件 |
| :-: |
| /* @file ToyBox.h */ |
| #ifndef _TOY_BOX |
| #define _TOY_BOX |
| #include "PlainBox.h" |

```
enum Color {BLACK, RED, BLUE, GREEN, YELLOW, WHITE};
template<class ItemType>
class ToyBox : public PlainBox<ItemType>
{
private:
   Color boxColor;
public:
   ToyBox();
   ToyBox(const Color& theColor);
   ToyBox(const ItemType& theItem, const Color& theColor);
   Color getColor() const;
}; // end ToyBox
#include "ToyBox.cpp"
#endif
```

ToyBox 类的实例有两个数据字段——继承的 item 和新的 boxColor。因为派生类的实例可以调用基类中的任何公共方法，ToyBox 的实例拥有 PlainBox 定义的所有方法；新的构造函数；一个新的编译器生成的析构函数；以及一个新方法 getColor。虽然派生类的实例包含继承数据字段的副本，但继承方法的代码不会被复制。
派生类不能直接访问基类的私有成员，即使它们被继承。继承并不意味着访问权。毕竟，你可以继承一个上锁的保险库，却无法打开它。在当前示例中，PlainBox 的数据字段 item 是私有的，因此你只能在 PlainBox 类的定义中引用它，而不能在 ToyBox 类的定义中引用它。但是，ToyBox 类可以使用 PlainBox 的公共方法 setItem 和 getItem 来间接设置或获取 item 的值。

```
LISTING C1-6 Implementation file for the class ToyBox
/** @file ToyBox.cpp */
template<class ItemType>
ToyBox<ItemType>::ToyBox()
{
   PlainBox<ItemType>();
   boxColor = BLACK;
} // end default constructor
template<class ItemType>
ToyBox<ItemType>::ToyBox(const Color& theColor)
{
   PlainBox<ItemType>();
   boxColor = theColor;
} // end constructor
template<class ItemType>
ToyBox<ItemType>::ToyBox(const ItemType& theItem,
                         const Color& theColor)
{
  PlainBox<ItemType>();
  setItem(theItem);
  boxColor = theColor;
} // end constructor

template<class ItemType>
Color ToyBox<ItemType>::getColor() const
{
  return boxColor;
} // end getColor
```

继承使你在定义新类时能够复用软件组件。我们的 ToyBox 类不继承 PlainBox 的构造函数，但它可以使用 PlainBox 的构造函数或方法来初始化 PlainBox 中的私有数据字段。要使用基类的默认构造函数，我们将语句

```
PlainBox<ItemType>();
```

放在每个 ToyBox 构造函数的第一条语句中。这确保基类中的数据字段被正确初始化。只能以这种方式调用默认构造函数。如果我们需要对设置基类数据字段有更多控制权，派生类构造函数必须调用适当的基类变更方法，如第三个 ToyBox 构造函数所示。在这种情况下，基类命名空间指示符应位于方法名称之前，以便编译器知道在哪里找到方法的定义。仅在构造函数中才需要使用命名空间指示符，如我们在实现 MagicBox 类时将看到的那样。

我们的 ToyBox 类的客户端可以以与 PlainBox 类非常相似的方式创建和使用 ToyBox 对象：

```
string favoriteToy = "Jack-in-the-Box";
ToyBox<string> myToyCase(favoriteToy, RED); // A red toy box
string oldToy = myToyCase.getItem(); // oldToy is a Jack-in-the-Box
favoriteToy = "Spinning Top";
myToyCase.setItem(favoriteToy); // myToyCase now holds a Spinning Top
```

### C1.4.2 重写基类方法

你可以向派生类添加任意数量的新成员。虽然你不能修改基类的私有数据字段，也不应修改它们的名称，但你可以重新定义继承的方法；这称为重写基类方法。如果派生类中的方法与基类中的方法具有相同的名称和参数声明——即具有相同的签名——则该方法会重写（或重新定义）基类中的方法。

要了解何时可能需要重新定义基类方法，让我们考虑 MagicBox 类的实现。这个盒子会神奇地将放入其中的任何物品变为它曾经持有的第一个物品的副本。实现此功能的简单方法是只存储第一个物品。对 setItem 的未来调用将不执行任何操作。因此，每次调用 getItem 都会返回盒子中存储的第一个物品。

与玩具盒一样，我们可以从 PlainBox 类派生我们的类，但我们还需要一个数据字段来指示是否已在盒子中存储初始物品。我们可以使用一个布尔字段 firstItemStored，一旦第一个物品存储在盒子中，它就被设置为 true。然后我们可以检查此标志以查看 setItem 应该做什么。如果 firstItemStored 为 false，我们知道传递给 setItem 的参数是我们被要求存储的第一个物品。如果 firstItemStored 为 true，我们知道这不是第一个物品，我们什么也不做。

以下是我们 MagicBox 方法的 UML 表示法：

```
+setItem(ItemType theItem)
+getItem(): ItemType
```

这些方法与 PlainBox 类中的方法类似，但我们需要不同的 setItem 实现来满足此盒子的特殊要求。因此，我们需要重写 PlainBox 中的 setItem 实现。清单 C1-7 给出了我们 MagicBox 类的头文件。它包含私有数据字段 firstItemStored、一个默认构造函数、一个参数化构造函数，以及我们需要的特殊版本的 setItem。

```
LISTING C1-7 Header file for the class MagicBox

/** @file MagicBox.h */
#ifndef _MAGIC_BOX
#define _MAGIC_BOX
#include "PlainBox.h"

template<class ItemType>
class MagicBox : public PlainBox<ItemType>
{
private:
   bool firstItemStored;
public:
   MagicBox();
   MagicBox(const ItemType& theItem);
   void setItem(const ItemType& theItem);
}; // end MagicBox

#include "MagicBox.cpp"
#endif
```

默认构造函数的实现必须调用基类构造函数，然后将数据字段 firstItemStored 初始化为 true，以指示第一个物品尚未存储。setItem 方法必须检查此数据字段，如果未存储任何物品，则调用基类方法 setItem 将参数存储在数据字段 item 中。你可以在清单 C1-8 中看到这些实现。

```
LISTING C1-8 Implementation file for the class MagicBox

/** @file MagicBox.cpp */
template<class ItemType>
MagicBox<ItemType>::MagicBox()
{
   PlainBox<ItemType>();
}
(continues)
```

