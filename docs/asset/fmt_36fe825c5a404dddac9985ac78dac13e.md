
在此声明中，成员变量 `width` 和 `length` 被声明为私有，这意味着它们只能通过类的成员函数访问。然而，成员函数被声明为公共，这意味着它们可以从类外的语句进行调用。如果类外的代码需要在 `Rectangle` 对象中存储宽度或长度，它必须通过调用对象的 `setWidth` 或 `setLength` 成员函数来实现。同样地，如果类外的代码需要检索存储在 `Rectangle` 对象中的宽度或长度，它必须通过调用对象的 `getWidth` 或 `getLength` 成员函数来实现。这些公共函数为类外的代码使用 `Rectangle` 对象提供了接口。

> 注意：尽管类的默认访问权限是私有的，但仍然使用 `private` 关键字来显式地声明私有成员仍然是一个好主意。这清晰地记录了类中所有成员的访问规范。

## 在成员函数中使用 const

注意 `const` 关键字出现在 `getWidth`、`getLength` 和 `getArea` 成员函数的声明中，如下：

```cpp
double getWidth() const;
double getLength() const;
double getArea() const;
```

当关键字出现在成员函数声明的括号之后时，它指定该函数不会更改调用对象中存储的任何数据。如果你不意中在函数中编写更改调用对象数据的代码，编译器将生成错误。正如你稍后看到的，`const` 关键字也必须出现在函数头中。

## 公共和私有成员的放置

没有规则要求你在声明公共成员之前声明私有成员。`Rectangle` 类可以如下被声明：

```cpp
class Rectangle {
    public:
    void setWidth(double);
    void setLength(double);
    double getWidth() const;
    double getLength() const;
    double getArea() const;
    private:
    double width;
    double length;
};
```

## 在访问器中使用 const

注意 `const` 关键字出现在 `getWidth`、`getLength` 和 `getArea` 成员函数的头中，如下所示：

```cpp
double Rectangle::getWidth() const
double Rectangle::getLength() const
double Rectangle::getArea() const
```

回想一下，这些函数在类中也使用 `const` 关键字进行了声明。当你将一个成员函数标记为 `const` 时，`const` 关键字必须同时出现在声明和函数头中。

从本质上说，当你将成员函数标记为 `const` 时，你是在告诉编译器调用对象是一个常量。如果你无意中在函数编写了更改调用对象的数据，编译器将生成错误。因为这减少了代码中出现 Bug 的概率，所以将所有访问函数标记为 `const` 是一个良好的做法。

## 数据隐藏的重要性

作为一名初学者，你可能会疑惑为什么要隐藏你创建的类内部的数据。当你学习编程时，你将是自己类的用户，因此这看起来就像是你正费尽很大精力向自己隐藏数据。然而，如果你在工业界编写软件，你创建的类将作为大型软件系统的组件被使用；你以外的程序员将使用你的类。通过隐藏类的数据并允许仅通过类的成员函数进行访问，你可以更好地确保该类按照你预期的方式运行。

## 定义类的实例

概念：类对象必须在类声明后进行定义。

和结构体变量一样，类对象在定义之前不会在内存中创建。这是因为类声明本身并不创建对象，而仅仅是对象的描述。我们可以使用它来创建一个或多个对象，这些对象就是类的实例。

类对象通过简单的定义语句创建，就像变量一样。这里是通用格式：`ClassName objectName;`

```cpp
ClassName objectName;
```

在通用格式中，`ClassName` 是类的名称，`objectName` 是我们赋予该对象的名字。

例如，以下语句将 `box` 定义为 `Rectangle` 类的对象：

```cpp
Rectangle box;
```

定义类对象被称为类的实例化。在这条语句中，`box` 是 `Rectangle` 类的一个实例。

![](img/191adf3284699566e6a7b1008ce9bdb5_764_0.png)

## 访问对象的成员

我们之前定义的 `box` 对象是 `Rectangle` 类的一个实例。假设我们想更改 `box` 对象中宽度变量的值。为了这样做，我们必须使用 `box` 对象来调用 `setWidth` 成员函数，如下所示：

```cpp
box.setWidth(12.7);
```

就像你使用点运算符访问结构体的成员一样，你也使用点运算符来调用类的成员函数。这条语句使用 `box` 对象调用 `setWidth` 成员函数，并将 `12.7` 作为参数传递。结果，`box` 对象的宽度变量将被设置为 `12.7`。这里是其他使用对象调用成员函数的语句示例：

```cpp
box.setLength(4.8);               // 将 box 的长度设置为 4.8。
x = box.getWidth();              // 将 box 的宽度赋值给 x。
cout << box.getLength();      // 显示 box 的长度。
cout << box.getArea();          // 显示 box 的面积。
```

> 笔记：注意，在 `Rectangle` 类的成员函数内部，没有使用点运算符来访问类的任何成员变量。当使用对象来调用成员函数时，该成员函数可以直接访问该对象的成员变量。

## 一个类演示程序

程序 13-1 是一个演示 `Rectangle` 类的完整程序。

### 程序 13-1

```cpp
1 // 此程序演示了一个简单的类。
2 #include <iostream>
3 using namespace std;
4
5 // Rectangle 类的声明。
6 class Rectangle
7 {
8   private:
9   double width;
10  double length;
11  public:
12  void setWidth(double);
13  void setLength(double);
14  double getWidth() const;
15  double getLength() const;
16  double getArea() const;
17 };
18
19 //************************************************
20 // setWidth 给 width 成员赋值。  *
21 //************************************************
22
23 void Rectangle::setWidth(double w)
24 { // 13.3 定义类的实例 733
25     width = w;
26 }
27 
28 //********************************************************************
29 // setLength 给 length 成员赋值。 
30 //********************************************************************
31 
32 void Rectangle::setLength(double len)
33 {
34     length = len;
35 }
36 
37 //********************************************************************
38 // getWidth 返回 width 成员的值。 
39 //********************************************************************
40 
41 double Rectangle::getWidth() const
42 {
43     return width;
44 }
45 
46 //********************************************************************
47 // getLength 返回 length 成员的值。 
48 //********************************************************************
49 
50 double Rectangle::getLength() const
51 {
52     return length;
53 }
54 
55 //********************************************************************
56 // getArea 返回 width 和 length 的乘积。 
57 //********************************************************************
58 
59 double Rectangle::getArea() const
60 {
61     return width * length;
62 }
63 
```

### 程序 13-2

```cpp
// 此程序创建了 Rectangle 类的三个实例。
#include <iostream>
using namespace std;
// Rectangle 类声明。
// 第 6 到 62 行已省略。
//********************************************************************
// 函数 main
//********************************************************************
int main() {
    double number;     // 用于存储一个数字
    double totalArea;   // 总面积
    Rectangle kitchen; // 存储厨房的尺寸
    Rectangle bedroom; // 存储卧室的尺寸
    Rectangle den; // 存储书房的尺寸
    // 获取厨房尺寸。
    cout << "What is the kitchen's length?";
    cin >> number;             // 获取长度
    kitchen.setLength(number); // 存储在 kitchen 对象中
    cout << "What is the kitchen's width?";
    cin >> number;             // 获取宽度
    kitchen.setWidth(number); // 存储在 kitchen 对象中
    // 获取卧室尺寸。
    cout << "What is the bedroom's length?";
    cin >> number;             // 获取长度
    bedroom.setLength(number); // 存储在 bedroom 对象中
    cout << "What is the bedroom's width?";
    cin >> number;             // 获取宽度
    bedroom.setWidth(number); // 存储在 bedroom 对象中
    // 获取书房尺寸。
    cout << "What is the den's length?";
    cin >> number;             // 获取长度
    den.setLength(number); // 存储在 den 对象中
    cout << "What is the den's width?";
    cin >> number;             // 获取宽度
    den.setWidth(number); // 存储在 den 对象中
    // 计算三个房间的总面积。
    totalArea = kitchen.getArea() + bedroom.getArea() + den.getArea();
    // 显示三个房间的总面积。
    cout << "The total area of the three rooms is " << totalArea << endl;
    return 0;
}
```

### 13.3 定义类的实例

```cpp
108 return;
109 }
```

#### 粗体显示的程序输出

```text
What is the kitchen's length? 10
What is the kitchen's width? 14
What is the bedroom's length? 15
What is the bedroom's width? 12
What is the den's length? 20
What is the den's width? 30
The total area of the three rooms is 92
```

在第 72、73 和 74 行，以下代码定义了三个 `Rectangle` 变量。这创建了三个 `Rectangle` 类的实例：

```cpp
Rectangle kitchen; // 存储厨房尺寸
Rectangle bedroom; // 存储卧室尺寸
Rectangle den; // 存储书房尺寸
```

在示例输出中，用户输入 10 和 14 作为厨房的长度和宽度，输入 15 和 12 作为卧室的长度和宽度，输入 20 和 30 作为书房的长度和宽度。图 13-9 显示了在存储这些值后对象的状态。

#### 图 13-9 厨房、卧室和书房对象的状态

| 厨房对象 | 卧室对象 | 书房对象 |
| --- | --- | --- |
| 长度: 10.0 | 长度: 15.0 | 长度: 20.0 |
| 宽度: 14.0 | 宽度: 12.0 | 宽度: 30.0 |

从图 13-9 可以看出，每个 `Rectangle` 类的实例都有自己的长度和宽度变量。类的每个实例都有自己的可以存储其值的成员变量。类的成员函数可以对特定的实例执行操作。查看程序 13-2 第 79 行的以下语句：

```cpp
kitchen.setLength(number);
```

此语句调用 `setLength` 函数，将值存储在 `kitchen` 对象的长度变量中。现在看第 87 行的以下语句：

```cpp
bedroom.setLength(number);
```

此语句也调用了 `setLength` 函数，但这次将值存储在 `bedroom` 对象的长度变量中。同样，第 95 行的以下语句调用了 `setLength` 函数，将值存储在 `den` 对象的长度变量中：

```cpp
den.setLength(number);
```

`Rectangle` 类的所有成员函数工作方式类似。

## 避免过时数据

在 `Rectangle` 中，`getLength` 和 `getWidth` 函数返回存储在成员变量中的值。`getArea` 函数返回计算结果。你可能会奇怪为什么 `Rectangle` 的面积没有存储在成员变量中（像长度和宽度那样）。因为面积的值取决于其他数据，当其他数据更改时，该值就过时了。如果将 `Rectangle` 的面积存储在成员变量中，一旦长度或宽度发生变化，该成员变量的值就会错误。在设计类时，应该注意不要在成员变量中存储可能过时的数据。相反，提供一个返回计算结果的成员函数。

## 指针

你也可以定义类的指针。例如，以下语句定义了一个名为 `rectPtr` 的指针变量：

```cpp
Rectangle *rectPtr = nullptr;
```

`rectPtr` 不是一个对象，但它可以持有 `Rectangle` 对象的地址。以下代码显示：

```cpp
Rectangle myRectangle;              // Rectangle 对象
Rectangle *rectPtr = nullptr;        // Rectangle 指针
rectPtr = &myRectangle;               // rectPtr 现在指向 myRectangle
```

第一条语句创建了一个 `Rectangle` 对象 `myRectangle`。第二条语句创建了一个名为 `rectPtr` 的 `Rectangle` 指针。第三条语句将 `myRectangle` 对象的地址存储在 `rectPtr` 指针中。如图 13-10 所示。

#### 图 13-10 rectPtr 指向 myRectangle 对象

![](img/191adf328469956e6a7b100ce9bdb5_771_0.png)

然后可以使用 `->` 运算符通过 `rectPtr` 指针调用成员函数。以下语句显示：

```cpp
rectPtr->setWidth(12.5);
rectPtr->setLength(4.8);
```
