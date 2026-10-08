
# `this` 指针

这是 C++ 中的一个重要概念，是一个适用于类作用范围内的保留关键字，包含对象的地址。换句话说，`this` 的值就是对象本身。在类方法内部，当你调用一个方法时，编译器会将此指针作为隐式参数发送：

```cpp
class Human
{
  private:
    // 私有声明
    void Talk(string Statement)
    {
      cout << Statement;
    }

public:

    void IntroduceSelf()
    {
      Talk("Bla");
    }
};
```

你在这里看到 `this` 指针用于打印到屏幕。实际上，编译器将 `this` 指针作为参数：

```cpp
void SetAge(int HumansAge)
{
  this->Age = HumansAge;
}
```

注意 `this` 指针被所有实例共享。如果你想使用实例，显式声明此。

# `sizeof()` 类

你学习了使用 `sizeof()` 来确定类的大小，包括某些边界的填充。它报告了每个实例占用的字节数。

## 列表 9.12 使用 `sizeof` 的结果

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: class MonsterDB
4: {
5: private:
6:   char* Buffer;
7:
8:   ~MonsterDB() {
9:     if (Buffer != NULL)
10:       delete [] Buffer;
11:   }
12:
13: public:
14:   MonsterDB(const char* input) {
15:     Buffer = new char[strlen(input) + 1];
16:     strcpy(Buffer, input);
17:   }
18:
19:   MonsterDB(const MonsterDB& other) {
20:     Buffer = new char[strlen(other.Buffer) + 1];
21:     strcpy(Buffer, other.Buffer);
22:   }
23:
24:   int GetLength() {
25:     return strlen(Buffer);
26:   }
27:
28:   const char* GetString() {
29:     return Buffer;
30:   }
31: };
32:
33: int main() {
34:   MonsterDB m1("Adam");
35:   MonsterDB m2("Eve");
36: 
37:   cout << "sizeof(MonsterDB) = " << sizeof(MonsterDB) << endl;
38:   cout << "sizeof(m1) = " << sizeof(m1) << endl;
39:   cout << "sizeof(m2) = " << sizeof(m2) << endl;
40: 
41:   cout << "m1 length: " << m1.GetLength() << endl;
42:   cout << "m2 length: " << m2.GetLength() << endl;
43: 
44:   cout << "m1 string: " << m1.GetString() << endl;
45:   cout << "m2 string: " << m2.GetString() << endl;
46: 
47:   return 0;
48: }
```

### 输出

```
sizeof(String) = 4
sizeof(FirstMan) = 4
sizeof(FirstWoman) = 4
sizeof(Human) = 12
sizeof(FirstMaleHuman) = 12
sizeof(FirstFemaleHuman) = 12
```

### 分析

只要示例包含如之前列表 9.9 所示的 `class MyString`（不包含大部分显示文本语句）以及 `Human` 的变体（该变体使用 `MyString` 存储 `Name` 并增加了一个用于 `Gender` 的 bool 参数），它就会被分配。

让我们从分析输出开始。你看到，对类使用 `sizeof()` 的结果与该类对象的结果相同。因此，`sizeof(MyString)` 与 `sizeof(..)` 相同，因为此类类消耗的字节数在编译时是固定的，并且在类定义时就已经已知。不要对 `FirstMan` 和 `FirstWoman` 的字节数相同感到惊讶，尽管一个包含亚当，另一个包含夏莉娃；它们是由 `MyString::Buffer` 存储的，该缓冲区是一个 `char*` 指针，指针的大小固定为 4 字节（在 32 位系统上），并且与指向的数据量无关。

尝试手动计算报告为 12 的 `Human` 的 `sizeof()`。第 53、54 和 55 行说明 `Human` 包含一个 `int`、一个 `bool` 和一个 `MyString`。参考列表 3.4 快速复内置类型消耗的字节，你知道在示例系统中，`int` 消耗 4 字节，`bool` 消耗 1 字节，`MyString` 消耗 4 字节，这些总和并不等于输出报告的 12。这是由于内存对齐（word padding）以及影响 `sizeof()` 结果的其他因素。

# `struct` 与 `class` 的区别

`struct` 是 C 时代的关键字，对于所有实际用途，C++ 编译器对其的处理方式与 `class` 非常相似。例外在于当程序员没有提到任何访问说明符时，不同的默认访问说明符（`public` 和 `private`）。因此，除非 `struct` 中的指定成员默认是公共的（`class` 默认是私有的），且在未指定的情况下，`struct` 具有来自基 `struct` 的公有继承（`class` 默认是私有的）。继承将在第 10 中详细讨论。

# 声明类的友

列表 9.12 中 `class Human` 的 `struct` 变体如下：

```
struct Human {
    // 构造函数，默认公有（因为没有提到访问说明符）
    Human(const MyString&InputName, int InputAge, bool InputGender)
    : Name(InputName), Age (InputAge), Gender(InputGender) {}

    int GetAge() {
        return Age;
    }

private:
    int Age;
    bool Gender;
    MyString Name;
};
```

你可以看到，`struct` 与 `class Human` 非常相似，实例化 `struct` 类型的对象与 `class` 类型类似：

`Human FirstMan("Adam", 25, true); // 是一个 struct 的实例`

# 声明类的友

类不允许外部访问其声明为私有的数据成员和方法。对于公开为友类或友函数的类和函数，这一规则被豁免，如列表 9.13 所示使用 `friend` 关键字。

**列表 9.13** 使用 `friend` 关键字允许外部函数 `DisplayAge()` 访问私有数据成员

```
0: #include <iostream>
1: #include <string>
2: using namespace std;
3:
4: class Human
5: {
6: private:
7:     string Name;
8:     int Age;
9:
10:    friend void DisplayAge(const Human& Person);
11:
12: public:
```

# 列表 9.13 继续

```
13:   Human(string InputName, int InputAge)
14:   {
15:     Name = InputName;
16:     Age = InputAge;
17:   }
18: };
19: 
20: void DisplayAge(const Human& Person)
21: {
22:     cout << Person.Age << endl;
23: }
24: 
25: int main()
26: {
27:   Human FirstMan("Adam", 25);
28:   cout << "Accessing private member Age via friend: ";

### 输出
Accessing private member Age via friend: 25

### 分析

第 10 行包含一个声明，指示编译器全局作用范围内的 `DisplayAge()` 允许访问类的私有成员。你可以注释掉第 10 行，以查看第 22 行立即失败。

像函数一样，外部类也可以被指定为友，如列表 9.14 所示。

# 列表 9.14 使用 `friend` 关键字允许外部类访问私有数据成员

```
0: #include <iostream>
1: #include <string>
2:   using namespace std;
3: 
4: class Human
5: {
6:   private:
7:     string Name;
8:     int Age;
9:
10:  friend class Utility;
11: 
12:  public:
13:     Human(string InputName, int InputAge)
14:     {
15:         Name = InputName;
16:         Age = InputAge;
17:     }
18: };
19: 
20: class Utility
21: {
22:     public:
23:     static void displayAge(const Human& Person)
24:     {
25:         cout << Person.Age << endl;
26:     }
27: };
28: 
29: int main()
30: {
31:   Human FirstMan("Adam", 25);
32:   cout << "Accessing private member Age via friend: ";
33:   Utility::displayAge(FirstMan);
34:   return 0;
35: }
```

### 输出
Accessing private member Age via friend: 25

### 分析

第 10 行包含了允许访问类的私有成员。这是由于内存对齐（word padding）以及影响 `sizeof()` 结果的其他因素。

## 总结

本课你学习了 `struct` 与 `class` 的区别、如何使用 `friend` 关键字以及私有成员。

# 第 9 课：类与对象

你学习了类的构造函数、如何通过构造函数实现设计模式。以及 访问说明符。

## 问答

- 类的实例和类之间有什么区别？
- 本质上没有。当你实例化类时，你得到了一个对象。
- 访问成员更好的方法是使用点运算符 (`.`) 还是指针运算符 (`->`)？
- 如果你有指针，指针运算符更合适。如果在栈上实例化类，点运算符更合适。
- 我应该总是编写构造函数吗？
- 如果你的类拥有智能指针`string` 类或 STL 容器（如 `std::vector`），你需要提供拷贝构造函数以确保深拷贝。
- 如果类只有一个定义的构造函数，这还是默认构造函数吗？
- 如果类可以不带参数创建，则该类有一个默认构造函数。
- 为什么某些示例使用 `SetAge()` 函数来设置 `Human::Age`？为什么不直接设为公有？
- 从技术角度来看，`Age` 公有也可以。但从设计角度来看，将成员数据私化是一个好主意。`getAge()` 或 `SetAge()` 等访问函数是访问私有数据的更优雅且可扩展的方法，允许你在设置 `Human::Age` 之前进行错误检查。

# 为什么拷贝函数的参数是引用拷贝源？

因为编译器期望拷贝构造函数是这种形式。背后的原因是，如果它按值接受拷贝源，它将调用自己，导致无限拷贝循环。

## 工作坊

工作坊提供的问题帮助你巩固对涵盖内容的理解，练习题为你提供所学知识的经验。在查看附录 D 中的答案之前，尝试回答测验和练习题，并在继续之前确保你理解了答案。

## 练习题

1. 找错：以下类声明中有什么错误？

```
Class Human
{
    int Age;
    string Name;
public:
    Human() {}
}
```

- 2. 练习 1 中该类的用户将如何访问成员 `Human::Age`？
- 3. 编写一个练习 1 中所示类的改进版本，在构造函数中使用初始化列表初始化所有参数。
- 4. 编写一个 `Circle` 类，它根据实例化时作为参数传递给类的半径计算面积和周长。`Pi` 应该包含在一个私有常量成员中，该成员无法从类外部访问。

# 第 10 节
## 实现继承

面向对象的编程基于四个重要方面：封装、抽象、继承和多态。继承是复用属性的一种强大方式，也是通多态的基石。

在本节中，你将了解到：

- 编程背景下的继承
- C++ 的继承语法
- 公（public）、私有（private）和保护（protected）继承
- 多重继承
- 隐藏基类方法和切割（slicing）引起的问题

## 继承的基础

Tom Smith 从祖先那里继承的首要的是姓氏，这让他成为了 Smith。此外，他还继承了父母教给他的某些价值观，以及 Smith 家族世世代代从事的雕塑专业。这些属性共同标识了 Tom 是 Smith 家族树的后代。

在编程中，你经常面临这样的情况：管理的组件具有相似的属性，但在细节或行为上存在微小差异。解决这个问题的方法之一是让每个组件成为一个类，每个类实现所有属性，甚至是重新实现公共属性。另一个解决方案是允许相似的类派自一个实现功能的基类，通过重写此基类功能来实现使每个类独有的行为。后者是首选方法。欢迎来到面向对象编程的继承世界，如图 10.1 所示。

图 10.1
类之间的继承。

![](img/fd01f923cb963a04200115e3b215851c_274_0.png)

### 继承与派生

图 10.1 显示了基类与其派生类之间的图示关系。要可视化基类或派生类可能并不容易，对吧？尝试理解派生类继承自基类，从这个意义上说它也是基类（就像 Tom 是 Smith 一样）。

注意

> 派生类与其基类之间的“是一个”（is-a）关系仅适用于公继承。本节从公继承开始，以理解继承的概念和最常见的继承形式，然后再转向私有或保护继承。

## 继承的基础

253

为了方便理解这个概念，设一个 `Bird`（鸟）类。`Crow`（乌鸦）、`Parrot`（鹦）或 `Kiwi`（奇异鸟）类派自 `Bird`。`Bird` 类将定义鸟的最基本属性，例如有羽毛、有翅膀、下蛋、会飞（大多数情况下）。派生类如 `Crow`、`Parrot` 或 `Kiwi` 继承它们的属性并对其进行自定义（例如，奇异鸟将不包含 `Fly()` 的实现）。表 10.1 展示了更多继承的例子。

表 10.1 取自日常生活的公继承示例

| 基类 | 示例派生类 |
| --- | --- |
| 鱼 (Fish) | 金鱼、鲤鱼、金枪鱼 (金枪鱼是鱼) |
| 哺乳动物 (Mammal) | 人、大象、狮子、鸭嘴兽 (鸭嘴兽是哺乳动物) |
| 鸟 (Bird) | 乌鸦、鹦、鸵、奇异鸟、鸭嘴兽 (鸭嘴兽是鸟类工具) |
| 形状 (Shape) | 圆、多边形 (圆是形状) |
| 多边形 (Polygon) | 三角形、八边形 (八边形是多边形，也是形状) |

这些示例说明当你戴上面向对象编程的眼镜时，你会在周围许多物体中看到继承的例子。鱼是金枪鱼的基类，因为金枪鱼像鲤鱼一样是鱼，并继承了冷血等鱼类特征。金枪鱼与鲤鱼的区别在于游泳的方式，以及它是咸水鱼。金枪鱼和鲤鱼通过基类属性来区分彼此。如图 10.2 所示。

图 10.2
金枪鱼、鲤鱼和鱼之间的层级关系。

![](img/fd01f923cb963a04200115e3b215851c_275_0.png)

鸭嘴兽会游泳，但是一种特殊的动物，具有哺乳动物特征（如用奶喂养幼崽）、鸟类特征（如下蛋）以及有毒特征。因此，可以想象鸭嘴兽类继承自两个基类 `Mammal` 和 `Bird`，以继承哺乳和鸟特征。这种继承形式被称为多重继承，将在后文中讨论。

### C++ 派生语法

如何从 `Fish` 继承 `Carp` 类，或者泛指从 `Base` 类继承 `Derived` 类？C++ 语法如下：

```cpp
// 声明基类
class Base {
    // 成员
};
// 声明派生类
class Derived {
    // 派生类成员
};
```

访问修符可以是公（最常用，用于“派生类是基类”关系）、私有或保护（用于“派生类拥有基类”关系）。

`Carp` 类派自 `Fish` 的继承表示为：

```cpp
class Fish {
    // Fish 的成员
};
class Carp:public Fish {
    // Carp 的成员
};
```
