
```cpp
int Dragon::attack(int targetArmour, int specialDamage)
{
```
```cpp
int useSpecial = rand() % 2; // 0 or 1

int damage;

if (useSpecial)

    damage = specialDamage;

else

    damage = getClawDamage();

return MAX(damage - targetArmour, 0);
```

//RedDragon.cpp
```cpp
#include <string>

using std::string;

class RedDragon : public Dragon
{
private:
    int fireDamage;
public:
    RedDragon(int textSize);
    int attack(int targetArmour);
    void defend(int damage);
    string getName() { return "Red Dragon"; }
};
```

```cpp
RedDragon::RedDragon(int textSize) : Dragon(theSize)
{
    fireDamage = 4 * get();
}
```

```cpp
int RedDragon::attack(int targetArmour)
{
    return RedDragon::attack(targetArmour, fireDamage);
}
```

```cpp
void RedDragon::defend(int damage)
{
    getHitPoints() == (damage - getArmour()) / 3;
}
```

//BlueDragon.cpp
```cpp
#include <string>

using std::string;

class BlueDragon : public Dragon
{
private:
    int iceDamage;
public:
    BlueDragon(int textSize);
    int attack(int targetArmour);
    void defend(int damage);
    string getName() { return "Blue Dragon"; }
};
```

```cpp
BlueDragon::BlueDragon(int theSize) : Dragon(theSize)
{
    iceDamage = 3 * getSize();
}
```

```cpp
int BlueDragon::attack(int targetArmour)
{
    return Dragon::attack(targetArmour, iceDamage);
}
```

```cpp
void BlueDragon::defend(int damage)
{
    getHitPoints() == (damage - getArmour()) / 2;
}
```

//BlackDragon.cpp
```cpp
#include <string>

using std::string;

class BlackDragon : public Dragon
{
private:
  int poisonDamage;
public:
  BlackDragon(int theSize);
  int attack(int targetArmour);
  void defend(int damage);
  string getName() { return "Black Dragon"; }
};
```

```cpp
BlackDragon::BlackDragon(int theSize) : Dragon(theSize)
{
  poisonDamage = getSize();
}
```

```cpp
int BlackDragon::attack(int targetArmour)
{
    return BlackDragon::attack(targetArmour, poisonDamage);
}
```

```cpp
void BlackDragon::defend(int damage)
{
    getHitPoints() == damage - getArmour();
}
```

//DragonLord.cpp
```cpp
#include <iostream>
#include <ctime>
#include <cstdlib>
#include "Dragon.cpp"
#include "RedDragon.cpp"
#include "BlueDragon.cpp"
#include "BlackDragon.cpp"
```

```cpp
int menuChoice();
int main (void)
{
    using std::srand;
    using std::time;
    using std::rand;
    using std::cout;
    srand((unsigned int)time(0));
    Dragon* dragons[3];
    int hp = 15;
    int armour = 2;
    int tempArmour;
    int tempAttack;
    dragons[0] = new RedDragon(rand() % 4 + 1);
    dragons[1] = new BlackDragon(rand() % 4 + 1);
    dragons[2] = new BlueDragon(rand() % 4 + 1);
    Dragon* d = dragons[rand() % 3];
    cout << "欢迎，骑士。\n";
    cout << "你必须营救公主。\n";
    cout << " 她被一条 ";
    cout << d->getName() << " 抓走了。\n";
    cout << "你必须击败这条龙。\n";
    cout << "你的生命值是: " << hp << "\n";
    while (d->isAlive() && hp > 0)
    {
        int choice = menuChoice();
        if (choice == 3) {
            goto RUN;
        } else if (choice == 1) {
            tempAttack = rand() % 4;
        }
        // ... 逻辑继续
    }
RUN:
    return 0;
}
```

`int RemoveElementAt(int location);`

`~Storage();`

此类存储了一个整数数组，并提供了添加、查看和删除元素的方法。但如果你想存储浮点数或字符，该怎么办呢？你必须复制前面的代码并将整数改为浮点数或字符，这将是低效的。或者，你可能会以某种方式将想要存储的数据类型作为参数传递。然后你可能需要使用 `switch` 语句来处理每情况。这会迅速变得复杂且难以管理。

解决此问题的最佳方案是使用模板。`Storage` 类的模板版本可以存储任何类型的数据。模板是将数据类型作为参数传递的简单方法，而不会让方法变得复杂难以管理。当你使用模板时，`Storage` 类如下：

```cpp
template<class T> class Storage {
  T* data;
  int numElements;
public:
  Storage();
  Storage(T* array, int num) :
    data(array), numElements(num) {}
  Storage(int num) : data = new int[num];
  void AddElement(T element);
  T ElementAt(int location);
  T RemoveElementAt(int location);
  ~Storage();
};
```

如你所见，这相当不同。你现在可能觉得它有点陌生，但很快你就会变得熟悉。唯一变化的是将 `int` 替换为 `T`（但不是所有的 `int` 实例），并在类之前立即添加了 `template<T>`。

`T` 的用法很容易解释。它们充当类决定存储的任何类型数据的占位符。因此，如果用户决定存储整数，那么所有 `T` 的实例都是 `int`。某些 `int` 的用法被保留了，是因为它们不是数据的一部分。其中一些仅用于元素数量（这应该始终是一个整数值）。

# C++ 编程：零基础入门，第二版

代码 `template<class T>` 告诉计算机该类使用了模板，并且 `T` 被用作所存储数据类型的占位符。即使你写的是 `class T`，`T` 也不一定是一个类。它可以是任何数据类型。

另一种思考模板的方法是将其看作参数列表。前面的示例有一个参数，`class T`。当使用 `Storage` 类时，用户将要存储的数据类型“几乎”作为一个参数传递。然后 `T` 被填充为该数据类型。如你所见，`class T` 就像一个参数声明。在这里，`class` 关键字以一种不同的方式使用，表示“数据类型”。因此，如果你愿意，可以使用 `typename` 关键字代替 `class`（它们在这里的含义相同）。

在第一行声明 `T` 后，你可以像使用任何其他名称（如 `int` 或 `float`）一样在类中的任何地方使用它。这意味着你可以声明新变量、指针、数组或任何你可能使用类型名称的内容。

当你从此类模板创建对象时，必须指定你将存储什么种类型的数据。这里有一个存储整数的示例：

`Storage<int> intStore;`

如你所见，为模板指定数据类型就像传递参数。当 `intStore` 被创建时，`int` 取代类中所有的 `T`。你可以像使用任何其他类的名称一样使用 `Storage<int>`。同样，你可以存储任何类型的数据：

`Storage<float> floatStore; // 存储浮点数`

`Storage<string> stringStore; // 存储字符串`

`Storage<Shape*> shapeStore; // 存储指向 Shape 的指针`

看看创建类模板的语法：

```cpp
template<class TypeName> class ClassName(
  ClassDeclaration
);
```

`TypeName` 是数据类型的任意占位符，`ClassName` 是类的名称，`ClassDeclaration` 是类的声明（就像第 5 章“与 OOP 斗争”中的普通类一样）。请记住，`TypeName` 可以是任何有效的标识符，但通常是一个单个大写字母，如 `T` 或 `C`。

# 第 8 章 使用模板

```cpp
template<class TypeName> return Class<TypeName>::methodName(args)
{
    methodImplementation
}
```

`TypeName` 是参数名称（例如 `T`），`methodImplementation` 是方法的实现。

由于构造函数的实现使用了两次类名（一次用于类名，一次用于方法名），你通常需要在每次使用类名后加上 `<TypeName>`。然而，这有点冗余，所以对于方法名，你不需要（但如果你喜欢，也可以这样做）。以下是在类模板外部实现的构造函数的语法：

```cpp
template<typename> ClassName<TypeName>(args)
{
    constructorImplementation
}
```

或者你可以使用这种更常见的语法：

```cpp
template<typename> ClassName<TypeName>::ClassName(args)
{
    constructorImplementation
}
```

两种方法完全相同。这取决于个人喜好。第一种方法比较正式，但第二种更常见。

> 注意 如果你正在创建一个类模板，我们建议在使用模板进行泛化之前，先解决所有的错误和设计缺陷。这种方法让编程变得容易得多。

# 使用模板参数

角括号内的声明（例如 `<class T>`）是模板参数。正如你所看到的，它的行为就像一个参数。事实上，你可以拥有任意数量的参数。

模板参数实用的一个例子是数组。注意，模板参数可以用于定义数组的大小，例如，特定数据类型的数组。这里是可能的外观示例：

```cpp
template<class T> class MyArray {
  T data[10];
};
```

模板参数的另一个用途是定义函数的返回类型。例如：

```cpp
template<class T> T add(T a, T b) {
  return a + b;
}
```

最后，模板参数可以用于定义函数的参数。例如：

```cpp
template<class T> void print(T a) {
  std::cout << a << std::endl;
}
```

# 初学者 C++ 编程，第二版

此函数交换两个指针的值。以下是一个你如何使用该函数的示例：

```
int x = 5;
int y = 6;
swap(int&x, &y);
```

现在 x 包含值 6，而 y 包含值 5。`<algorithm>` 包含了该函数的标准库版本，名为 *swap*，它接受两个相同类型的参数（无论是哪种类型，因为标准库的 swap 是一个函数模板）。

# 理解参数解析

函数模板与类模板并不完全相同。对于函数模板，当你调用函数时，并不总是需要提供模板参数。有时，计算机仅仅就能根据你传递的参数推断出参数应该是什么。这里有一个示例：

```
add(5,3);
```

勇敢的读者，不要被误骗了；这不是第 4 章中的 `add` 函数。这里调用的是带有模板的版本。因为两个参数都是整数，计算机可以推断出参数 (T) 应该是 int。现在，你正在进入真正的编程领域；然而，目前你甚至不需要知道 add 函数有一个模板。你只需要像调用任何其他函数一样调用它即可。

如果前一个函数的参数不明确（例如，一个是整数而另一个是浮点数），编译器将返回错误。计算机的智能有限，它们无法决定应该将整数转换为浮点数还是将浮点数转换为整数。如果你选择不为函数模板调用提供参数，请确保参数能够明确指定参数应该是什么。

此外，如果并不是所有参数都包含在参数列表中（例如，有一个参数仅用于返回类型），你必须为函数调用提供完整的参数列表。

现在，作为一个案例研究，你已经准备好创建一个为你进行类型转换的函数（在第 2 章中，我们将类型转换定义为数据从一种类型转换为另一种类型的操作，保留几乎相同的值）。

此函数是一个参数未包含在参数列表中的示例，如下：

```
template<class C, class T> cast(T a)
{
    return (C)a;
}
```

该函数仅在普通转换对该参数有效时才起作用。以下是你可能如何使用该函数的示例：

```
cout << cast<int, float>(3.5); //将 3.5 转换为 3
cout << cast<float, int>(9); //将 9 转换为 9.0
```

```
//错误无法将 int 转换为 char*
cout << cast<char*, int>(35769);
```

在某些情况下，你可以根据函数参数推断第二个模板参数是什么。然而，对于默认函数参数，你可以只在参数列表末尾保留一个模板参数。例如，如果有三个参数，只要它们是可以假设的，你可以省略最后一个、两个或全部。以下是你如何省略参数的示例：

```
//将 3 转换为 3.0 - 第二个参数推断为 int
cout << cast<float>(3);
```

```
//将 3.5 转换为 3 - 第二个参数假设为 float
cout << cast<int>(3.5);
```

```
//错误 - 转换为什么？
cout << cast(35);
```

# 模板特化

有时，你可能希望模板针对特定类型的数据以特殊方式工作。某种数据类型可能是其他类型所遵循规则的例外。在这种情况下，你必须为该特定类型提供不同的模板版本。这个不同的版本被称为特化（specialization）。每当你使用该数据类型时，就可以使用它。

在本章后面的“使用 Vector”部分中，你将学习 vector。vector 是一个类模板。以下是 vector 类模板的基本声明：

```
template<class T> class Vector;
```

# 初学者 C++ 编程，第二版

这个声明看起来非常简单。它只是一个普通的模板。然而，vector 类模板除了这个更通用的声明外，还有一个特化。vector 必须以某种方式特殊处理 void 指针数组。以下是 Vector 类特化的声明：

```
template<> class Vector<void*>;
```

前面的代码本质上表示了 Vector 的特化，每当 void* 被作参数类型时，就会使用它。也就是说，当你将 void* 作为参数时，就会使用该特化版本。特化版本基本上接管了。如果你使用任何其他类型，则将使用第一个版本。以下是使用特化的示例：

```
#include <iostream>
#include <string>
```
