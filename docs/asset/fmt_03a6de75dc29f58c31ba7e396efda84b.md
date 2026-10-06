
# C++ 编程：从问题分析到程序设计 [第5版]

这些是非合法的枚举类型，因为没有任何一个值是标识符。

然而，以下是合法的枚举类型：

如果一个值已经在某个枚举类型中使用，则它不能在同一个块的任何其他枚举类型中使用。同样的规则也适用于在任何块之外定义的枚举类型。示例 8–4 阐了这一概念。

## 示例 8-4

考虑以下语句：

```
enum mathStudent {JOHN, BILL, CINDY, LISA, RON};
enum compStudent {SUSAN, CATHY, JOHN, WILLIAM}; //非法
```

假设这些语句位于同一个程序的同一个块中。第二个枚举类型 `compStudent` 是不允许的，因为值 `JOHN` 已经在之前的枚举类型 `mathStudent` 中被使用了。

### 声明变量

一旦定义了类型，你就可以声明该类型的变量。声明枚举类型变量的语法与之前相同：

```
dataType identifier, identifier,...,;
```

语句：

```
enum sports {BASKETBALL, FOOTBALL, HOCKEY, BASEBALL, SOCCER,
VOLLEYBALL};
```

定义了一个名为 `sports` 的枚举类型。语句：

`popularSport, mySport;`

将 `popularSport` 和 `mySport` 声明为类型 `sports` 的变量。

### 赋值

一旦声明了变量，你就可以在其中存储值。假设前面的声明，语句：

```
popularSport = FOOTBALL;
```

将 `FOOTBALL` 存储在 `popularSport` 中。语句：

`mySport = popularSport;`

将 `popularSport` 的值 copies 复制到 `mySport` 中。

### 枚举类型的操作

枚举类型不允许进行算术运算。因此，以下语句是非法的：

```
mySport = popularSport + 2;               //非法
popularSport = FOOTBALL + SOCCER;     //非法
popularSport = popularSport * 2;       //非法
```

此外，枚举类型不允许进行自增和自减操作。因此，以下语句是非法的：

```
popularSport++;               //非法
popularSport--;               //非法
```

假设你想将 `popularSport` 的值加 1。你可以使用类型转换运算符：

```
popularSport = static_cast<sports>(popularSport + 1);
```

当使用该名称时，编译器假设用户理解其正在做什么。因此，前面的语句会被编译，并且在执行期间，它会将 `popularSport` 的值推进到列表中的下一个值。考虑以下语句：

```
popularSport = FOOTBALL;
popularSport = static_cast<sports>(popularSport + 1);
```

在第二个语句之后，`popularSport` 的值为 `HOCKEY`。同样，将 `BASKETBALL` 存储在 `popularSport` 中的结果如下：

```
popularSport = FOOTBALL;
popularSport = static_cast<sports>(popularSport - 1);
```

结果是将 `BASKETBALL` 存储在 `popularSport` 中。

### 关系运算符

由于枚举是一个有序的值集合，关系运算符可以与枚举类型一起使用。同样假设你拥有之前定义的 `sports` 枚举类型以及变量 `popularSport` 和 `mySport`。那么：

```
FOOTBALL <= SOCCER true
HOCKEY > BASKETBALL true
BASEBALL < FOOTBALL false
```

假设：

```
popularSport = SOCCER;
mySport = VOLLEYBALL;
```

那么：

```
popularSport < mySport is true
```

### 枚举类型与循环

回想枚举类型是一种整类型，使用类型转换运算符（即 `operator (type, name)`），你可以递增、递减和比较枚举类型的值。因此，你可以在循环中使用这些枚举类型。假设 `mySport` 是之前声明的变量。考虑以下 `for` 循环：

```
for (mySport = BASKETBALL; mySport < SOCCER;
mySport = static_cast<sports>(mySport + 1))
```

这个 `for` 循环有五次迭代。在循环中使用枚举增加了程序的可读性。

### 枚举类型的输入/输出

由于输入和输出只定义了 `int`、`char` 等内置类型，枚举类型既不能直接输入也不能直接输出。然而，你可以间接地进行。假设你拥有以下语句：

```
enum courses {ALGEBRA, ANALYSIS, BASIC, CHEMISTRY, HISTORY, PASCAL, PHILOSOPHY};
```

为了输入，例如使用以下结构：

```cpp
char ch1, ch2;

cout << "Enter the two letters of the course: " << endl;
cin >> ch1 >> ch2;

switch (ch1)
{
    case 'a':
    case 'A':
        if (ch2 == 'l' || ch2 == 'L')
            registered = ALGEBRA;
        else
            registered = ANALYSIS;
        break;
    case 'b':
    case 'B':
        registered = BASIC;
        break;
    case 'c':
    case 'C':
        if (ch2 == 'h' || ch2 == 'H')
            registered = CHEMISTRY;
        else
            registered = CPP;
        break;
    case 'h':
    case 'H':
        registered = HISTORY;
        break;
    case 'p':
    case 'P':
        if (ch2 == 'a' || ch2 == 'A')
            registered = PASCAL;
        else
            registered = PHILOSOPHY;
        break;
    default:
        cout << "Illegal input." << endl;
}
```

同样，你可以直接输出枚举类型：

```cpp
switch (registered)
{
    case ALGEBRA:
        cout << "Algebra";
        break;
    case ANALYSIS:
        cout << "Analysis";
        break;
    case BASIC:
        cout << "Basic";
        break;
    case CHEMISTRY:
        cout << "Chemistry";
        break;
    case CPP:
        cout << "CPP";
        break;
    case HISTORY:
        cout << "History";
        break;
    case PASCAL:
        cout << "Pascal";
        break;
    case PHILOSOPHY:
        cout << "Philosophy";
        break;
}
```

### 函数与枚举类型

你可以像其他简单类型一样将枚举类型传递给函数——即通过值或引用。此外，就像简单类型一样，函数也可以返回枚举类型的值。通过这种机制，你可以使用函数来输入枚举类型。假设枚举类型定义之前：

```cpp
courses readCourse()
{
    courses registered;
    char ch1, ch2;

    cout << "Enter the two letters of the course: " << endl;
    cin >> ch1 >> ch2;

    switch (ch1)
    {
        case 'a':
        case 'A':
            if (ch2 == 'l' || ch2 == 'L')
                registered = ALGEBRA;
            else
                registered = ANALYSIS;
            break;
        case 'b':
        case 'B':
            registered = BASIC;
            break;
        case 'c':
        case 'C':
            if (ch2 == 'h' || ch2 == 'H')
                registered = CHEMISTRY;
            else
                registered = CPP;
            break;
        case 'h':
        case 'H':
            registered = HISTORY;
            break;
        case 'p':
        case 'P':
            if (ch2 == 'a' || ch2 == 'A')
                registered = PASCAL;
            else
                registered = PHILOSOPHY;
            break;
        default:
            cout << "Illegal input." << endl;
    }
    return registered;
}
//end readCourse
```

以下函数输出一个枚举类型值：

```cpp
void printEnum(courses registered)
{
    switch (registered)
    {
        case ALGEBRA:
            cout << "Algebra";
            break;
        case ANALYSIS:
            cout << "Analysis";
            break;
        case BASIC:
            cout << "Basic";
            break;
        case CHEMISTRY:
            cout << "Chemistry";
            break;
        case CPP:
            cout << "CPP";
            break;
        case HISTORY:
            cout << "History";
            break;
        case PASCAL:
            cout << "Pascal";
            break;
        case PHILOSOPHY:
            cout << "Philosophy";
            break;
    }
}
```

```cpp
case CPP:
out << "CPP";
break;
case HISTORY:
out << "History";
break;
case PASCAL:
out << "Pascal";
break;
case PHILOSOPHY:
out << "Philosophy";
break;
} // switch
//end printEnum
```

### 在定义枚举类型时声明变量

在之前的章节中，你首先定义了一个枚举，然后声明了该类型的变量。C++ 允许你将这些步骤合并为一。也就是说，你可以在定义枚举类型的同时声明该枚举类型的变量。例如，语句：

```cpp
enum {A, B, C, D, F} courseGrade;
```

这定义了一个枚举类型 `grades`，并声明了一个类型为 `grades` 的变量 `courseGrade`。

同样，该语句：

```cpp
enum {PENNY, NICKEL, DIME, HALFDOLLAR, DOLLAR} change, usCoins;
```

这定义了一个枚举类型 `coins`，并声明了两个类型为 `coins` 的变量 `change` 和 `usCoins`。

### 匿名数据类型

在变量声明中直接指定值而没有名称的数据类型被称为匿名类型。以下语句创建了一个匿名类型：

```cpp
enum {BASKETBALL, FOOTBALL, BASEBALL, HOCKEY} mySport;
```

该语句指定了值并声明了变量 `mySport`，但没有给数据类型命名。

然而，创建匿名类型有缺点。首先，由于该类型没有名称，你无法将匿名类型作为参数传递给函数，函数也无法返回匿名类型的值。其次，在一个匿名类型中使用的值可以在另一个匿名类型中使用，但这些类型的变量处理方式不同。考虑以下语句：

```cpp
enum {ENGLISH, FRENCH, SPANISH, GERMAN, RUSSIAN} languages;
enum {ENGLISH, FRENCH, SPANISH, GERMAN, RUSSIAN} foreignLanguages;
```

尽管变量 `languages` 和 `foreignLanguages` 具有相同的值，但编译器将它们视为不同类型的变量。因此，以下语句是非法的：

```cpp
languages = foreignLanguages; // 非法
```

尽管可以使用这些功能，但使用时要谨慎。为了避免混淆，请先定义枚举类型并声明变量。

我们将描述 C++ 中的 `typedef` 语句。

### typedef 语句

在 C++ 中，你可以使用 `typedef` 语句为之前定义的数据类型创建别名或代号。`typedef` 语句的一般语法为：

```cpp
typedef existingTypeName newTypeName;
```

在 C++ 中，`typedef` 是一个关键字。注意，`typedef` 语句不会创建任何数据类型；它只创建现有数据类型的别名。

> 示例 8-6

语句：

`typedef int integer;`

为数据类型 `int` 创建了别名 `integer`。同样，该语句：

`typedef double real;`

为数据类型 `double` 创建了别名 `real`。该语句：

`typedef double decimal;`

为数据类型 `double` 创建了别名 `decimal`。

使用 `typedef` 语句，你可以创建自己的布尔数据类型，如 8-7 所示。

> 示例 8-7

回想第 4 章，记得 C++ 中的逻辑（布尔）表达式求的值为 1 或 0，这些实际上是 `int` 值。作为一个逻辑值，1 代表真，0 代表假。考虑以下语句：

![](img/b08b54ded82fc9e3d8d95107a5b40e44_7_0.png)

```cpp
typedef int Boolean; // 第1行
const Boolean TRUE = 1; // 第2行
const Boolean FALSE = 0; // 第3行
Boolean flag; // 第4行
```

第 1 行的语句为数据类型 `int` 创建了别名 `Boolean`。第 2 行和第 3 行的语句声明了命名常量 `TRUE` 和 `FALSE`，并分别将它们初始化为 1 和 0。第 4 行的语句声明 `flag` 为 `Boolean` 类型的变量。因为 `flag` 是 `Boolean` 类型的变量，以下语句是：

```cpp
flag = TRUE;
```

### 编程示例：剪刀石头布游戏

孩子们经常玩剪刀石头布游戏。这个游戏有两个玩家，每个人选择三个物体中的一个：石头、纸或剪刀。如果玩家 1 选择石头而玩家 2 选择纸，则玩家 2 赢得游戏，因为纸盖住石头。游戏按照以下规则进行：

- 如果两个玩家都选择同一个物体，则平局。
- 如果一个玩家选择石头而另一个选择剪刀，则选择石头的人胜，因为石头可以打碎剪刀。
- 如果一个玩家选择石头而另一个选择纸，则选择纸的人胜，因为纸盖住石头。
- 如果一个玩家选择剪刀而另一个选择纸，则选择剪刀的人胜，因为剪刀可以剪纸。

编写一个交互式程序，允许两个玩家玩这个游戏。

- 用户在被要求玩游戏时的响应。
- 玩家的选择。

输入 此程序有两种类型的输入：

输出 玩家的选择以及每局的获胜者。游戏结束后，应该输出总局数和该玩家胜的次数。
