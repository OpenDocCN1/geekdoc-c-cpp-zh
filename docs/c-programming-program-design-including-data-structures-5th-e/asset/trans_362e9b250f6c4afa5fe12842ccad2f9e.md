
## 食材

### 面团：

- 2杯中筋面粉
- 1茶匙盐
- 1汤匙橄榄油
- 3/4杯温水

### 顶料：

- 1/2杯番茄酱
- 1杯切碎的马苏里拉奶酪
- 新鲜罗勒叶

## 制作说明

- 1. 在碗中混合面粉和盐。
- 2. 加入橄榄油和温水；揉至光滑。
- 3. 让面团静置30分钟。
- 4. 将面团擀开，抹上番茄酱。
- 5. 撒上奶酪和罗勒。
- 6. 在220°C下烘烤15分钟。

编写一个程序，提示用户输入：

- a. 河流宽度
- b. 工厂在河对岸下游的距离
- c. 在水下铺设电线的成本
- d. 在陆地上铺设电线的成本

然后程序输出应水下铺设的电线长度和应陆上铺设的电线长度，以使建造电线的成本最低。程序还应输出建造电线的总成本。

## 16. **（管道问题，需要三角学）**

一根管道需要绕过两条相交走廊的直角拐角搬运。假设两条相交走廊的宽度分别为5英尺和8英尺（见图7-22）。你的目标是求出能够水平绕过直角拐角搬运的最长管道的长度，并四舍五入到最接近的英尺。

![](img/f97f778697507bb6fdd80c5991210cba_473_0.png)

**图7-22** 管道问题

编写一个程序，提示用户输入两条走廊的宽度。然后程序输出能够水平绕过直角拐角搬运的最长管道的长度，并四舍五入到最接近的英尺。（注意，管道长度由 \(l = AB + BC = 8 / \sin\theta + 5 / \cos\theta\) 给出，其中 \(0 < \theta < \pi/2\)。）

![](img/f97f778697507bb6fdd80c5991210cba_474_0.png)

## 第8章

## 用户定义的简单数据类型、命名空间和`string`类型

本章中，你将：

- 学习如何创建和操作自己的简单数据类型——枚举类型
- 熟悉`typedef`语句
- 了解`namespace`机制
- 探索`string`数据类型，并学习如何使用各种`string`函数来操作字符串

在第2章中，你了解到C++的简单数据类型分为三类：整型、浮点型和`enum`。在后续章节中，你主要使用整型和浮点型数据类型。在本章中，你将学习`enum`类型。此外，语句`using namespace std;`（在第2章中讨论过）用于每个使用ANSI/ISO标准C++风格头文件的C++程序中。本章后半部分将考察这条语句的用途。实际上，你将了解`namespace`机制是什么。你还将学习`string`类型以及许多可用于有效操作字符串的有用函数。

### 枚举类型

> 本节可以跳过，不会影响内容的连续性。

第2章将数据类型定义为一组值以及对这些值的一组操作。例如，`int`数据类型由从-2,147,483,648到2,147,483,647的整数以及对这些数字的一组操作——即算术运算（+、-、*、/和%）——组成。由于程序的主要目标是操作数据，数据类型的概念对任何编程语言都变得至关重要。通过提供数据类型，你指定了哪些值是合法的，并告诉用户允许对这些值进行哪些操作。因此，系统为你提供了内置的错误检查。

到目前为止，你使用过的数据类型主要是`int`、`bool`、`char`和`double`。尽管这些数据类型足以解决几乎任何问题，但有时会出现这些数据类型不足以解决特定问题的情况。C++为用户提供了一种机制来创建自己的数据类型，这大大增强了编程语言的灵活性。

在本节中，你将学习如何创建自己的简单数据类型，即枚举类型。在后续章节中，你将学习更高级的技术来创建复杂的数据类型。

要定义**枚举类型**，你需要以下各项：

- 数据类型的名称
- 数据类型的一组值
- 对值的一组操作

C++允许你定义一个新的简单数据类型，在其中指定其名称和值，但不能指定操作。阻止用户创建自己的操作有助于避免潜在的系统故障。

你为数据类型指定的值必须是标识符。

枚举类型的语法是：

```cpp
enum typeName {value1, value2, ...};
```

其中value1、value2、……是称为**枚举器**的标识符。在C++中，**enum**是保留字。

通过在大括号之间列出所有值，你还指定了值之间的顺序。即，value1 < value2 < value3 < ……。因此，枚举类型是一个有序的值集合。此外，分配给这些枚举器的默认值从0开始。也就是说，分配给value1的默认值是0，分配给value2的默认值是1，依此类推。（你可以在定义枚举类型时为枚举器分配不同于默认值的其他值。）还要注意，枚举器value1、value2、……*不是*变量。

### 例8-1

语句：

```cpp
enum colors {BROWN, BLUE, RED, GREEN, YELLOW};
```

定义了一个名为colors的新数据类型，属于该数据类型的值是BROWN、BLUE、RED、GREEN和YELLOW。

### 例8-2

语句：

```cpp
enum standing {FRESHMAN, SOPHOMORE, JUNIOR, SENIOR};
```

将standing定义为枚举类型。属于standing的值是FRESHMAN、SOPHOMORE、JUNIOR和SENIOR。

### 例8-3

考虑以下语句：

```cpp
enum grades {'A', 'B', 'C', 'D', 'F'}; //illegal enumeration type
enum places {1ST, 2ND, 3RD, 4TH};   //illegal enumeration type
```

这些是非法的枚举类型，因为没有一个值是标识符。但是，以下是合法的枚举类型：

```cpp
enum grades {A, B, C, D, F};
enum places {FIRST, SECOND, THIRD, FOURTH};
```

如果一个值已经在一个枚举类型中使用过，那么同一块中的任何其他枚举类型都不能使用它。同样的规则适用于在任何块之外声明的枚举类型。例8-4说明了这一概念。

### 例8-4

考虑以下语句：

```cpp
enum mathStudent {JOHN, BILL, CINDY, LISA, RON};
enum compStudent {SUSAN, CATHY, JOHN, WILLIAM}; //illegal
```

假设这些语句位于同一程序中的同一块中。第二个枚举类型compStudent是不允许的，因为值JOHN已在之前的枚举类型mathStudent中使用过。

### 声明变量

一旦定义了数据类型，就可以声明该类型的变量。声明enum类型变量的语法与之前相同：

```cpp
dataType identifier, identifier,...;
```

语句：

```cpp
enum sports {BASKETBALL, FOOTBALL, HOCKEY, BASEBALL, SOCCER,
             VOLLEYBALL};
```

定义了一个名为sports的枚举类型。语句：

```cpp
sports popularSport, mySport;
```

将popularSport和mySport声明为sports类型的变量。

### 赋值

一旦声明了变量，就可以在其中存储值。假设有前面的声明，语句：

```cpp
popularSport = FOOTBALL;
```

将FOOTBALL存储到popularSport中。语句：

```cpp
mySport = popularSport;
```

将popularSport的值复制到mySport中。

### 枚举类型的操作

枚举类型不允许进行算术运算。因此以下语句是非法的：

```cpp
mySport = popularSport + 2;                //illegal
popularSport = FOOTBALL + SOCCER;          //illegal
popularSport = popularSport * 2;           //illegal
```

此外，枚举类型不允许递增和递减操作。因此以下语句是非法的：

```cpp
popularSport++; //illegal
popularSport--; //illegal
```

假设你想将popularSport的值递增1。可以如下使用强制类型转换运算符：

```cpp
popularSport = static_cast<sports>(popularSport + 1);
```

当使用类型名时，编译器假定用户明白自己正在做什么。因此，前面的语句会被编译，并在执行期间将popularSport的值推进到列表中的下一个值。考虑以下语句：

```cpp
popularSport = FOOTBALL;
popularSport = static_cast<sports>(popularSport + 1);
```

在第二条语句之后，popularSport的值是HOCKEY。类似地，语句：

```cpp
popularSport = FOOTBALL;
popularSport = static_cast<sports>(popularSport - 1);
```

结果是将BASKETBALL存储到popularSport中。

### 关系运算符

由于枚举是一个有序的值集合，关系运算符可以与枚举类型一起使用。再次假设你有前面定义的枚举类型sports以及变量popularSport和mySport。那么：

```cpp
FOOTBALL <= SOCCER is true
HOCKEY > BASKETBALL is true
BASEBALL < FOOTBALL is false
```
