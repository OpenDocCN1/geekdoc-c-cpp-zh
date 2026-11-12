

{
  item = theItem;
} // end setItem

ItemType PlainBox::getItem() const
{
  return item;
} // end getItem

头文件 PlainBox.h 包含我们的类声明。我们必须使用预处理器指令 #include 来包含 PlainBox 类声明，以便编译器可以验证我们的方法头并提供对类数据字段的访问。方法头必须与类声明中提供的方法头匹配。包含头文件并不会告诉编译器此处定义的方法属于 PlainBox 类。要做到这一点，你必须在构造函数和方法名称之前加上类名，后跟两个冒号——即，

```
PlainBox::
```

提出此要求的原因是，C++ 允许一个源文件包含多个类和独立函数的方法实现。命名空间指示符 PlainBox:: 是一个前缀，用于向编译器指示该方法属于 PlainBox 命名空间。C++ 命名空间是一种语法结构（例如类），允许你在一个通用名称（例如 PlainBox）下将数据和方法的声明分组在一起。一旦某个方法被定义为命名空间的一部分，它就可以访问该命名空间中的所有数据和方法。因此，清单 C1-2 中的构造函数和方法可以访问 PlainBox 的数据字段和方法。

> 注意：为了更好地模块化我们的代码，本书中的实现文件将仅包含单个类的方法。

## C.1.3 模板

此时，我们的 PlainBox 类与你可能在之前的 C++ 课程中实现过的许多类很相似。只要游戏中的角色想要在盒子中存储一个 double 值，该类就能正常工作。但如果一个角色想要存储一个 double，而另一个角色有一个字符串或 MagicWand 对象要存储，我们该怎么办呢？由于我们当前的 PlainBox 类只能存储一个 double，我们需要创建新类——例如 PlainBoxForStrings 和 PlainBoxForWands——来存储不同的对象类型。这些类的功能与 PlainBox 类完全相同，因此我们可以只做少量更改来复制代码。例如，我们需要更改每个头文件中的 typedef。对于 PlainBoxForStrings 类，typedef 将是

```
typedef string ItemType;
```

而对于 PlainBoxForWands 类，typedef 将是

```
typedef MagicWand ItemType;
```

我们还需要更改构造函数和命名空间指示符的名称，以反映新的类名。如果类更复杂，这些更改将需要大量工作，并且容易出错。后来，如果我们的朋友更改了 PlainBox 的要求，我们需要遍历每个 PlainBox 类变体并进行所需的更改。

此场景问题的根源在于，程序员必须在程序构建之前知道盒子中将存储什么类型的对象。然后，程序员必须为要存储的每种对象类型编写不同的类。每个盒子的功能相同，但数据类型不同。模板使程序员能够将实现的功能与类中使用的数据类型分开。清单 C1-3 包含 PlainBox 类模板版本的头文件。

### 清单 C1-3 PlainBox 类的模板头文件

```
/** @file PlainBox.h */
#ifndef _PLAIN_BOX
#define _PLAIN_BOX
template<class ItemType>; // Indicates this is a template definition
// Declaration for the class PlainBox
class PlainBox
{
private:
   // Data field
   ItemType item;
public:
   // Default constructor
   PlainBox();
   // Parameterized constructor
   PlainBox(const ItemType& theItem);
   // Mutator method that can change the value of the data field
   void setItem(const ItemType& theItem);
   // Accessor method to get the value of the data field
   ItemType getItem() const;
}; // End PlainBox
#include "PlainBox.cpp" // Include the implementation file
#endif
```

如清单 C1-3 所示，将我们在清单 C1-1 中之前定义的 PlainBox 类更改为模板，只需在头文件中更改一行：移除了 typedef，并用一条语句替换它，以指示这是一个模板类：

```
template<class ItemType>;
```

然而，我们还必须在 #endif 指令之前包含实现文件，方法是编写

```
#include "PlainBox.cpp"
```

此添加是必要的，因为编译器在看到模板的客户端实例化并知道与数据类型参数 ItemType 对应的实际数据类型之前，不会编译模板类。

**编程提示：** 在你的开发环境中，不要将实现文件（例如 PlainBox.cpp）添加到项目中。它将在需要时自动包含。

实现文件 PlainBox.cpp 需要进行一些更改，但这些更改都遵循一种模式。在每个方法定义之前，你都要编写相同的模板语句：

```
template<class ItemType>;
```

以指示该方法是一个模板。命名空间指示符 PlainBox<ItemType>:: 也必须位于每个方法名称之前，以反映该方法的定义基于 ItemType。这些更改在清单 C1-4 中显示。

```
LISTING C1-4 Implementation file for the PlainBox template class
/* @file PlainBox.cpp */
template<class ItemType>;
PlainBox<ItemType>::PlainBox()
{ // end default constructor
template<class ItemType>;
PlainBox<ItemType>::PlainBox(const ItemType& theItem)
{
item = theItem;
} // end constructor
template<class ItemType>;
void PlainBox<ItemType>::setItem(const ItemType& theItem)
{
item = theItem;
} // end setItem
template<class ItemType>;
ItemType PlainBox<ItemType>::getItem() const
{
return item;
} // end getItem
```

要实例化一个 PlainBox 实例，你需要写出要放入盒子中的项目的数据类型，并用尖括号括起来：

```
PlainBox<double> numberBox; // A box to hold a double
PlainBox<string> nameBox; // A box to hold a string object
PlainBox<MagicWand> wandBox; // A box to hold a MagicWand object
```

这些盒子实例的方法调用方式与之前相同：

```
double health = 6.5;
numberBox.setItem(health);
string secretName = "Rumpelstiltskin";
nameBox.setItem(secretName);
MagicWand elfWand;
wandBox.setItem(elfWand);
```

> 注意：通过使用模板，你可以定义一个涉及任何类型数据的类，甚至包括在你设计和实现类之后才创建的数据类型。

## C.1.4 继承

既然 PlainBox 类已经编写完成，我们将来看另外两个盒子。玩具盒与我们的普通盒子非常相似，但它有一个额外的特性——颜色，我们可以使用枚举类型 Color 来表示它。我们在创建玩具盒时设置其颜色。游戏中的角色可以询问盒子的颜色，但不能更改它。以下是这些方法的 UML 表示法：

```
+getColor(): string
+setItem(ItemType theItem)
+getItem(): ItemType
```

setItem 和 getItem 方法的行为与为 PlainBox 类实现的同名方法完全相同。我们可以通过使用继承来重用 PlainBox 中的代码。继承允许我们重用和扩展已经完成和测试过的工作。

### C.1.4.1 基类和派生类

我们可以将 PlainBox 用作 ToyBox 类的基类（或超类）。你可以将基类视为父类。ToyBox 类是 PlainBox 类的派生类（或子类）。要指示 ToyBox 从 PlainBox 派生，我们在 ToyBox 的类头中使用以下语法：

```
class ToyBox : public PlainBox<ItemType>
```

派生类的任何实例也被视为基类的实例，可以在程序中任何可以使用基类实例的地方使用。另外，当使用关键字 public 与基类一起时，基类中公开定义的任何方法或数据字段都可以在派生类的实例中使用。在 C++ 中，派生类继承其基类的所有成员，除了构造函数和析构函数。也就是说，派生类除了它自己定义的成员外，还拥有基类的数据字段和方法，尽管它只能访问公开定义的成员。派生类还可以修改任何继承的公共方法。

如清单 C1-5 所示，如果 ToyBox 不需要修改基类的任何方法，它只定义特定于它自己的构造函数和新方法。setItem 和 getItem 方法从 PlainBox 类继承，可以在我们的 ToyBox 类中使用。

```
LISTING C1-5 Template header file for the class ToyBox
// @file ToyBox.h */
#ifndef TOY_BOX
#define TOY_BOX
#include "PlainBox.h"
```

