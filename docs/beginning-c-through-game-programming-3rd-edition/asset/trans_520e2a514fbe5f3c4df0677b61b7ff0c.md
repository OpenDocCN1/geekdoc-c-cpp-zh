

需要。如果你在成员函数中不需要更改任何数据成员，那么最好将该成员函数声明为常量。它可以防止你在成员函数中意外地修改数据成员，并且能让其他程序员清楚你的意图。

## 陷阱

好吧，我撒了点小谎。常量成员函数可以修改静态数据成员。你将在本章稍后学习静态数据成员，具体在“声明和初始化静态数据成员”一节。还有，如果你用 mutable 关键字限定一个数据成员，那么即使是常量成员函数也可以修改它。现在，先不用担心这两个例外。

你可以通过在函数头部的末尾加上关键字 const 来声明一个常量成员函数。这就是我在 Critter 中所做的，如以下行所示，它将 GetHunger() 声明为常量成员函数。

```
int GetHunger() const;
```

这意味着 GetHunger() 不能更改 Critter 类中声明的任何非静态数据成员的值，也不能调用任何非常量的 Critter 成员函数。我将 GetHunger() 设为常量，因为它只返回一个值并且不需要修改任何数据成员。一般来说，Get 成员函数可以定义为常量。

## 使用静态数据成员和成员函数

对象很棒，因为每个实例都存储自己的数据集合，使其具有独特的身份。但如果想要存储有关整个类的一些信息，比如存在的实例总数怎么办？你可能想这样做，如果你创建了一堆敌人，并且希望它们根据总数来攻击玩家。例如，如果总数低于某个阈值，你可能希望敌人逃跑。你可以在每个对象中存储实例总数，但这会浪费存储空间。而且，随着总数的变化，更新所有对象也会很麻烦。相反，你真正想要的是为整个类存储一个单一值的方式。你可以用静态数据成员来实现这一点。

## 介绍 Static Critter 程序

Static Critter 程序声明了一种新型的 critter，它有一个静态数据成员来存储已创建的 critter 总数。它还定义了一个静态成员函数来显示总数。在程序实例化任何新的 critter 对象之前，它通过直接访问保存总数的静态数据成员来显示 critter 的总数。接下来，程序实例化了三个新的 critter。然后它通过调用访问静态数据成员的静态成员函数来显示 critter 的总数。图 8.4 显示了程序的结果。

![](img/34f09be0ed6217c465debc4490197d4f_292_0.png)

图 8.4
程序将 Critter 对象的总数存储在静态数据成员 s_Total 中，并以两种不同的方式访问该数据成员。

你可以从 Course Technology 网站 (www.courseptr.com/downloads) 下载此程序的代码。该程序位于第 8 章文件夹中；文件名是 static_critter.cpp。

```
//Static Critter
//Demonstrates static member variables and functions

#include <iostream>

using namespace std;

class Critter
{
public:
    static int s_Total;      //static member variable declaration
                            //total number of Critter objects in existence

    Critter(int hunger = 0);
    static int GetTotal();  //static member function prototype

private:
    int m_Hunger;
};

int Critter::s_Total = 0;   //static member variable initialization

Critter::Critter(int hunger):
    m_Hunger(hunger)
{
    cout << "A critter has been born!" << endl;
    ++s_Total;
}

int Critter::GetTotal()      //static member function definition
{
    return s_Total;
}

int main()
{
    cout << "The total number of critters is: ";
    cout << Critter::s_Total << "\n\n";

    Critter crit1, crit2, crit3;

    cout << "\nThe total number of critters is: ";
    cout << Critter::GetTotal() << "\n";

    return 0;
}
```

## 声明和初始化静态数据成员

静态数据成员是为整个类存在的一个单一数据成员。在类定义中，我声明了一个静态数据成员 s_Total 来存储已实例化的 Critter 对象数量。

```
static int s_Total;    //static member variable declaration
```

你可以像我一样声明自己的静态数据成员，只需以 static 关键字开头声明即可。我在变量名前面加上了 s_，以便可以立即识别为静态数据成员。

在类定义之外，我将静态数据成员初始化为 0。

```
int Critter::s_Total = 0;    //static member variable initialization
```

注意我用 Critter:: 限定了数据成员名。在其类定义之外，你必须用其类名限定静态数据成员。执行完上一行代码后，与 Critter 类关联有一个单一值，存储在其静态数据成员 s_Total 中，值为 0。

## 提示

你也可以在非类函数中声明静态变量。静态变量在函数调用之间保持其值。

## 访问静态数据成员

你可以在程序的任何地方访问公共静态数据成员。在 main() 中，我用以下行访问 Critter::s_Total，它显示 0，即静态数据成员的值，也是已实例化的 Critter 对象的总数。

```
cout << Critter::s_Total << "\n\n";
```

## 提示

你也可以通过该类的任何对象访问静态数据成员。假设 crit1 是一个 Critter 对象，我可以用以下行显示 critter 的总数：

```
cout << crit1.s_Total << "\n\n";
```

我也在 Critter 构造函数中使用以下行访问此静态数据成员，它递增 s_Total。

```
++s_Total;
```

这意味着每次实例化一个新对象时，s_Total 都会递增。注意我没有用 Critter:: 限定 s_Total。就像非静态数据成员一样，在其类内部你不需要用类名限定静态数据成员。

虽然我将静态数据成员设为 public，但你可以将静态数据成员设为 private——然后，像其他任何数据成员一样，你只能在类成员函数中访问它。

## 声明和定义静态成员函数

静态成员函数为整个类存在。我在 Critter 中用以下行声明了一个静态成员函数：

```
static int GetTotal();  //static member function prototype
```

你可以像我一样声明自己的静态成员函数，只需以 static 关键字开头声明即可。静态成员函数通常编写为与静态数据成员一起工作。

我定义了静态成员函数 GetTotal()，它返回静态数据成员 s_Total 的值。

```
int Critter::GetTotal()    //static member function definition
{
    return s_Total;
}
```

静态成员函数定义与迄今为止看到的非静态成员函数定义非常相似。主要区别在于静态成员函数不能访问非静态数据成员。这是因为静态成员函数为整个类存在，并且与类的任何特定实例无关。

## 调用静态成员函数

在 main() 中实例化三个 Critter 对象后，我再次用以下行显示 critter 的总数，它显示 3。

```
cout << Critter::GetTotal() << "\n\n";
```

为了正确标识静态成员函数，我必须用 Critter:: 限定它。要从其类之外调用静态成员函数，你必须用其类名限定它。

## 提示

你也可以通过该类的任何对象访问静态成员函数。假设 crit1 是一个 Critter 对象，我可以用以下行显示 critter 的总数：

```
cout << crit1.GetTotal() << "\n\n";
```

由于静态成员函数为整个类存在，你可以在没有任何类实例存在的情况下调用静态成员函数。而且，就像私有静态数据成员一样，私有静态成员函数只能被同一类的其他成员函数访问。

## 介绍 Critter Caretaker 游戏

Critter Caretaker 游戏让玩家负责自己的虚拟宠物。玩家完全负责让 critter 保持快乐，这可不是一件小事。他可以喂养和陪玩 critter 来保持它心情良好。他还可以倾听 critter 来了解 critter 的感受，这可以从快乐到生气不等。图 8.5 展示了游戏。

![](img/34f09be0ed6217c465debc4490197d4f_296_0.png)

## 图 8.5

如果你未能喂养或娱乐你的 critter，它的心情会变差。（但别担心——在适当的照顾下，你的 critter 可以恢复到阳光般的心情。）

