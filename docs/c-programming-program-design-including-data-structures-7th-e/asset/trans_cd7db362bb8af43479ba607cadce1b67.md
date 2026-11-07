

示例 10-1 说明了如何访问类的成员。

## 示例 10-1

假设我们有如下声明（例如，在用户程序中）：

```cpp
clockType myClock;
clockType yourClock;
```

考虑以下语句：

```cpp
myClock.setTime(5, 2, 30);
myClock.printTime();
yourClock.setTime(x, y, z);    //assume x, y, and z are
                              //variables of type int
if (myClock.equalTime(yourClock))
.
.
.
```

这些语句是合法的；也就是说，它们在语法上是正确的。

在第一条语句 myClock.setTime(5, 2, 30); 中，成员函数 setTime 被执行。值 5、2 和 30 作为参数传递给函数 setTime，该函数使用这些值将 myClock 的三个成员变量 hr、min 和 sec 的值分别设置为 5、2 和 30。类似地，第二条语句执行成员函数 printTime，并输出 myClock 的三个成员变量的内容。在第三条语句中，变量 x、y 和 z 的值用于设置 yourClock 的三个成员变量的值。

在第四条语句中，成员函数 equalTime 执行，并将 myClock 的三个成员变量与 yourClock 的对应成员变量进行比较。因为在这条语句中 equalTime 是对象 myClock 的成员，所以它可以直接访问 myClock 的三个成员变量。因此，它还需要另一个对象来进行比较，在本例中这个对象就是 yourClock。本质上，equalTime 需要两个对象进行比较。它通过点运算符作用的对象 myClock 是一个，而参数 yourClock 是另一个。这解释了为什么函数 equalTime 只有一个参数。

对象 myClock 和 yourClock 只能访问类 clockType 的公有成员。因此，以下语句是非法的，因为 hr 和 min 被声明为类 clockType 的私有成员，因而不能由对象 myClock 和 yourClock 访问。

```cpp
myClock.hr = 10;                  //illegal
myClock.min = yourClock.min;  //illegal
```

### 类的内置操作

C++ 的大多数内置操作不适用于类。你不能使用算术运算符对类对象执行算术运算（除非它们被重载；见第 13 章）。例如，你不能使用运算符 + 将两个类对象相加，比如 clockType 类型的对象。此外，你不能使用关系运算符比较两个类对象是否相等（除非它们被重载；见第 13 章）。

对类对象有效的两种内置操作是成员访问（.）和赋值（=）。你已经看到如何通过使用类对象名、然后一个点、然后成员名来访问类的单个成员。（例如，如果 myClock 是一个 clockType 对象，那么在语句 `myClock.incrementSeconds();` 中，myClock 访问成员 incrementSeconds。）

现在我们借助一个例子来说明赋值语句如何工作。

### 赋值运算符与类

假设 myClock 和 yourClock 是如前定义的 clockType 对象。此外，假设 myClock 和 yourClock 的值如图 10-3(a) 所示。

![](img/d0be7fc6d804b63484835c6c8bc67a07_707_0.png)

**图 10-3** *执行语句 myClock = yourClock; 之前和之后的 myClock 和 yourClock*

语句：

```cpp
myClock = yourClock;      //Line 1
```

将 yourClock 的值复制到 myClock 中。也就是说，

- yourClock.hr 的值被复制到 myClock.hr，
- yourClock.min 的值被复制到 myClock.min，以及
- yourClock.sec 的值被复制到 myClock.sec。

换句话说，yourClock 的三个成员变量的值被复制到 myClock 的对应成员变量中。因此，赋值语句执行的是逐成员复制。第 1 行中的语句执行后，myClock 和 yourClock 的值如图 10-3(b) 所示。

### 类作用域

类对象可以是自动的（即每次控制流到达其声明时创建，并在控制流退出外围块时销毁），也可以是静态的（即只创建一次，在控制流到达其声明时创建，并在程序终止时销毁）。此外，你还可以声明类对象数组。类对象与其他变量具有相同的作用域。类的成员与结构体的成员具有相同的作用域。也就是说，类的成员在类内是局部的。在类外访问类成员时，使用类对象名和成员访问运算符（.）。

### 函数与类

以下规则描述了函数与类之间的关系：

- 类对象可以作为参数传递给函数，也可以作为函数值返回。
- 作为函数参数，类对象既可以按值传递，也可以按引用传递。
- 如果类对象按值传递，则实参的成员变量内容会被复制到形参的对应成员变量中。

### 引用参数与类对象（变量）

回想一下，当变量按值传递时，形参会复制实参的值。也就是说，会为形参分配用于复制实参值的内存空间。类对象作为参数时可以按值传递。

假设一个类有几个成员变量，需要大量内存来存储数据，而你需要按值传递一个变量。相应的形参随后会接收该变量数据的一份副本。也就是说，编译器必须为形参分配内存，以便复制实参的成员变量的值。除了需要大量存储空间外，这个操作还可能花费相当多的计算机时间，将实参的值复制到形参中。

另一方面，如果变量按引用传递，形参只接收实参的地址。因此，将变量作为参数传递的一种高效方式是按引用传递。如果变量按引用传递，那么当形参改变时，实参也会改变。然而，有时你不希望函数能够更改成员变量的值。在 C++ 中，你可以按引用传递变量，同时通过在形参声明中使用关键字 const 来防止函数更改其值。例如，考虑下面的函数定义：

```cpp
void testTime(const clockType& otherClock)
{
    clockType dClock;
    .
    .
    .
}
```

函数 testTime 包含一个引用参数 otherClock。参数 otherClock 使用关键字 const 声明。因此，在调用函数 testTime 时，形参 otherClock 接收实参的地址，但 otherClock 不能修改实参的内容。例如，在以下语句执行后，myClock 的值不会被改变：

```cpp
testTime(myClock);
```

事实上，如果函数 testTime 试图修改 otherClock，编译器将生成语法错误。

通常，如果你想将类对象声明为值参数，可以如前所述，使用关键字 const 将其声明为引用参数。

回想一下，如果形参是值参数，那么在函数定义内，你可以更改形参的值。也就是说，你可以使用赋值语句更改形参的值（当然，这不会影响实参）。然而，如果形参是常量引用参数，那么你不能在函数内使用赋值语句更改其值，也不能使用任何其他函数更改其值。因此，在函数 testTime 的定义内，你不能改变 otherClock 的值。例如，在函数 testTime 的定义中，以下语句将是非法的：

```cpp
otherClock.setTime(5, 34, 56); //illegal
otherClock = dClock;           //illegal
```

### 成员函数的实现

当我们定义类 clockType 时，只包含了成员函数的函数原型。为了使这些函数正常工作，我们必须编写相关算法。实现这些函数的一种方式是在类本身中提供函数定义而不是函数原型。不幸的是，这样类定义会变得非常长且难以理解。提供函数原型而不是函数定义的另一个原因与信息隐藏有关；也就是说，我们希望隐藏对数据操作的细节。我们将在本章后面的“信息隐藏”一节中讨论这个问题。

