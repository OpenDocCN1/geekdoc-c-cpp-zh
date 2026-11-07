
- 另一方面，假设一个 `class`，比如 dummyClass，包含带参数的构造函数，但不包含默认构造函数。在这种情况下，C++ 不会为 `class` dummyClass 提供默认构造函数。因此，当声明 `class` dummyClass 的对象时，必须在其声明中包含适当的实参。

下面的代码进一步说明了这一点。考虑以下类的定义：

```cpp
class dummyClass
{
public:
    void print() const;

    dummyClass(int dX, int dY);

private:
    int X;
    int Y;
};
```

`class` dummyClass 没有默认构造函数。它有一个带参数的构造函数。给定 `class` dummyClass 的这一定义，以下对象声明是合法的：

```cpp
dummyClass myObject(10, 25);   //Object declaration is legal
```

然而，由于 `class` dummyClass 不包含默认构造函数，以下声明是不正确的，并且会产生语法错误：

```cpp
dummyClass dummyObject;   //incorrect object declaration
```

因此，为避免此类陷阱，如果一个类有构造函数，该类也应包含默认构造函数。

## 类对象（变量）数组与构造函数

如果一个类有构造函数，并且你声明了该类对象组成的数组，那么该类应具有默认构造函数。默认构造函数通常用于初始化每个（数组中的）类对象。

例如，如果你声明一个包含 100 个类对象的数组，那么为每个分量指定不同的构造函数是不切实际的（甚至是不可能的）。（我们将在本节末尾进一步说明这一点。）

假设你有 100 名按小时计酬的员工，并且需要记录他们的到达和离开时间。你可以声明两个数组——arrivalTimeEmp 和 departureTimeEmp——每个数组包含 100 个分量，其中每个分量都是 clockType 类型的对象。

考虑以下语句：

```cpp
clockType arrivalTimeEmp[100];              //Line 1
```

第 1 行中的语句创建了对象数组 arrivalTimeEmp[0]、arrivalTimeEmp[1]、……、arrivalTimeEmp[99]，如图 11-8 所示。

![](img/f97f778697507bb6fdd80c5991210cba_668_0.png)

![](img/f97f778697507bb6fdd80c5991210cba_669_0.png)

**图 11-8** 数组 arrivalTimeEmp

现在你可以使用 `clockType` 类的函数来操作每位员工的时间。例如，以下语句将第 50 位员工的到达时间，即 hr、min 和 sec，分别设置为 8、5 和 10（见图 11-9）。

```cpp
arrivalTimeEmp[49].setTime(8, 5, 10);    //Line 2
```

![](img/f97f778697507bb6fdd80c5991210cba_669_1.png)

**图 11-9** 设置员工 49 的时间后的数组 arrivalTimeEmp

要输出每位员工的到达时间，可以使用循环，如下所示：

```cpp
for (int j = 0; j < 100; j++)                         //Line 3
{
    cout << "Employee " << (j + 1)
         << " arrival time: ";
    arrivalTimeEmp[j].printTime();                    //Line 4
    cout << endl;
}
```

第 4 行中的语句以 `hr:min:sec` 的形式输出一名员工的到达时间。

要记录每位员工的离开时间，可以使用数组 departureTimeEmp。

类似地，你可以使用数组来管理姓名列表或其他对象。

> **注意**
>
> 在结束关于类对象数组的讨论之前，我们想指出以下内容：本节开头指出，如果你声明一个类对象数组，并且该类有构造函数，那么该类应具有默认构造函数。编译器使用默认构造函数来初始化对象数组。如果数组规模很大，那么为每个对象指定一个不同的带参数构造函数是不切实际的。对于小规模数组，我们可以设法指定一个不同的带参数构造函数。

例如，以下语句将 clocks 声明为一个包含两个分量的数组。第一个分量的成员变量分别初始化为 8、35 和 42。第二个分量的成员变量分别初始化为 6、52 和 39。

```cpp
clockType clocks[2] = {clockType(8, 35, 42), clockType(6, 52, 39)};
```

事实上，表达式 clockType(8, 35, 42) 创建了 clockType 类的一个匿名对象；将其成员变量分别初始化为 8、35 和 42；然后使用逐成员复制来初始化对象 clocks[0]。

考虑以下语句，它创建对象 myClock，并将其成员变量分别初始化为 10、45 和 38。这就是我们一直以来创建和初始化对象的方式。事实上，语句：

```cpp
clockType myClock(10, 45, 38);
```

等价于语句：

```cpp
clockType myClock = clockType(10, 45, 38);
```

然而，第一条语句更高效。它不需要先创建一个匿名对象，然后再逐成员复制以初始化 myClock。

我们在这里强调的要点，也是我们在上一节中讨论过的内容，如下：为避免任何陷阱，如果一个类有构造函数，它也应具有默认构造函数。

## 析构函数

与构造函数一样，析构函数也是函数。此外，与构造函数一样，析构函数没有类型。也就是说，它既不是有返回值的函数，也不是 void 函数。然而，一个类只能有一个析构函数，并且析构函数没有参数。析构函数的名字是波浪号字符（~），后跟类名。例如，clockType 类的析构函数名为：

```cpp
~clockType();
```

当类对象超出作用域时，析构函数会自动执行。析构函数的用法将在后续章节中讨论。

## 数据抽象、类和抽象数据类型

对于我们驾驶的汽车，大多数人想知道如何启动汽车并驾驶它。大多数人不关心发动机工作原理的复杂性。通过将汽车发动机的设计细节与其使用分开，制造商帮助驾驶员专注于如何驾驶汽车。我们的日常生活中还有其他类似的例子。大多数情况下，我们只关心如何使用某些物品，而不关心它们如何工作。

将设计细节（即汽车发动机如何工作）与其使用分开称为**抽象**。换句话说，抽象关注发动机做什么，而不是它如何工作。因此，抽象是将逻辑属性与实现细节分离的过程。驾驶汽车是一种逻辑属性；发动机的构造构成实现细节。我们对发动机做什么有抽象的看法，但对发动机的实际实现不感兴趣。

抽象也可以应用于数据。本章前面的小节定义了数据类型 clockType。数据类型 clockType 有三个成员变量以及以下基本操作：

- 1. 设置时间。
- 2. 返回时间。
- 3. 打印时间。
- 4. 将时间增加一秒。
- 5. 将时间增加一分钟。
- 6. 将时间增加一小时。
- 7. 比较两个时间，看它们是否相等。

这些操作的实际实现，即 clockType 类的成员函数的定义，被推迟了。

数据抽象被定义为将数据的逻辑属性与其实现分离的过程。clockType 的定义及其基本操作是逻辑属性；将 clockType 对象存储在计算机中以及执行这些操作的算法是 clockType 的实现细节。

**抽象数据类型（ADT）：** 一种将逻辑属性与实现细节分离的数据类型。

像任何其他数据类型一样，ADT 有三样与之关联的内容：ADT 的名称，称为**类型名**；属于该 ADT 的值的集合，称为**域**；以及对该数据的操作集合。按照这些约定，我们可以如下定义 clockType ADT：

```cpp
dataTypeName
    clockType
domain
    Each clockType value is a time of day in the form of hours,
    minutes, and seconds.
operations
    Set the time.
    Return the time.
    Print the time.
    Increment the time by one second.
    Increment the time by one minute.
    Increment the time by one hour.
    Compare the two times to see whether they are equal.
```

### 示例 11-7

列表被定义为同一类型的值的集合。因为列表中的所有值都是同一类型，所以表示和处理列表的一种便捷方式是使用数组。你可以如下将一个列表定义为一个 ADT：

```cpp
dataTypeName
    listType
domain
    Every listType value is an array of, say, 1000 numbers
operations
    Check to see whether the list is empty.
    Check to see whether the list is full.
    Search the list for a given item.
    Delete an item from the list.
    Insert an item in the list.
    Sort the list.
    Destroy the list.
    Print the list.
```

下一个显而易见的问题是如何在程序中实现 ADT。要实现一个 ADT，你必须表示数据并编写算法来执行这些操作。

上一节使用类将数据和函数组合在一起。此外，我们对类的定义只包含操作的规范；实现操作的函数是单独编写的。因此，我们看到类是实现 ADT 的一种便捷方式。事实上，在 C++ 中，类就是专门为处理 ADT 而设计的。

