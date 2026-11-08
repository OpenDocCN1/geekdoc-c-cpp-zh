
类型为`studentType`的指针变量，`*studentPtr`指向一个类型为`studentType`的内存空间，该类型是一个结构体。因此，`(*studentPtr).gpa`引用该结构体的`gpa`成员。

考虑表达式`*studentPtr.gpa`。让我们看看这个表达式是如何求值的。因为`.`（点运算符）的优先级高于`*`，所以`studentPtr.gpa`先求值。`studentPtr.gpa`会产生语法错误，因为`studentPtr`不是结构体变量，它没有名为`gpa`的成员。

如你所见，在表达式`(*studentPtr).gpa`中，括号很重要。然而，输入错误可能会带来问题。因此，为了简化通过指针访问类或结构体成员的操作，C++提供了另一种运算符，称为**成员访问运算符箭头**，即`->`。运算符`->`由两个连续的符号组成：一个连字符和一个“大于”号。

使用运算符`->`访问类（结构体）成员的语法是：

```text
pointerVariableName->classMemberName
```

因此，语句：

```cpp
(*studentPtr).gpa = 3.9;
```

等价于语句：

```cpp
studentPtr->gpa = 3.9;
```

因此，通过指针使用运算符`->`访问类（结构体）成员，既不需要括号，也不需要解引用运算符。由于输入错误不可避免，而缺少括号可能导致程序异常终止或错误结果，因此本书在通过指针访问类（结构体）成员时使用箭头表示法。

示例12-4说明了指针如何与类成员函数配合使用。

## 示例12-4

考虑以下类：

```cpp
class classExample
{
public:
    void setX(int a);
        //Function to set the value of x
        //Postcondition: x = a;
    void print();
        //Function to output the value of x

private:
    int x;
};
```

成员函数的定义如下：

```cpp
void classExample::setX(int a)
{
    x = a;
}
void classExample::print() const
{
    cout << "x = " << x << endl;
}
```

考虑以下main函数：

```cpp
int main()
{
    classExample *cExpPtr;       //Line 1
    classExample cExpObject;     //Line 2

    cExpPtr = &cExpObject;       //Line 3

    cExpPtr->setX(5);            //Line 4
    cExpPtr->print();            //Line 5

    return 0;
}
```

### 示例运行：

```text
x = 5
```

在main函数中，第1行的语句将cExpPtr声明为classExample类型的指针，第2行的语句将cExpObject声明为classExample类型的对象。第3行的语句将cExpObject的地址存储到cExpPtr中（见图12-3）。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_834_0.png)

图12-3  执行语句`cExpPtr = &cExpObject;`后的cExpObject和cExpPtr

在第4行的语句中，指针`cExpPtr`访问成员函数`setX`来设置成员变量`x`的值（见图12-4）。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_835_0.png)

**图12-4** 执行语句`cExpPtr->setX(5);`后的`cExpObject`和`cExpPtr`

在第5行的语句中，指针`cExpPtr`访问成员函数`print`来打印`x`的值，如上所示。

## 初始化指针变量

由于C++不会自动初始化变量，如果你不希望指针变量指向任何东西，就必须对它们进行初始化。指针变量使用常量值0进行初始化，该值称为**空指针**。因此，语句`p = 0;`将空指针存储到`p`中，也就是说，`p`不指向任何东西。有些程序员使用命名常量`NULL`来初始化指针变量。以下两条语句是等价的：

```cpp
p = NULL;
p = 0;
```

数字0是唯一可以直接赋值给指针变量的数字。

## 动态变量

在前面的章节中，你学习了如何声明指针变量，如何将变量的地址存储到与其类型相同的指针变量中，以及如何使用指针操作数据。然而，你学到的使用指针操作数据仅限于使用其他变量创建的内存空间。换句话说，指针是在已有的内存空间中操作数据。那么，使用指针的好处是什么呢？你可以通过操作创建这些内存空间的变量来访问它们。在本节中，你将了解指针背后的强大功能。具体来说，你将学习如何在程序执行期间使用指针分配和释放内存。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_835_1.png)

在程序执行期间创建的变量称为**动态变量**。在指针的帮助下，C++创建动态变量。C++提供了两个运算符`new`和`delete`，分别用于创建和销毁动态变量。当程序需要新变量时，使用运算符`new`。当程序不再需要某个动态变量时，使用运算符`delete`。

在C++中，`new`和`delete`是保留字。

## 运算符`new`

运算符`new`有两种形式：一种用于分配单个变量，另一种用于分配数组变量。使用运算符`new`的语法是：

```cpp
new dataType;              // to allocate a single variable
new dataType[intExp];      // to allocate an array of variables
```

其中`intExp`是任何求值为正整数的表达式。

运算符`new`分配指定类型的内存（变量）并返回一个指向它的指针——即所分配内存的地址。而且，所分配的内存是未初始化的。

考虑以下声明：

```cpp
int *p;
char *q;
int x;
```

语句：

```cpp
p = &x;
```

将x的地址存储在p中。但是，没有分配新的内存。另一方面，考虑以下语句：

```cpp
p = new int;
```

该语句在程序执行期间在内存中的某处创建了一个变量，并将所分配内存的地址存储在p中。所分配的内存通过指针解引用来访问，即`*p`。类似地，语句：

```cpp
q = new char[16];
```

创建了一个包含16个char类型元素的数组，并将数组的基地址存储在q中。

由于动态变量是未命名的，因此无法直接访问。它通过`new`返回的指针间接访问。以下语句说明了这一概念：

```cpp
int *p;                 //p is a pointer of type int
char *name;             //name is a pointer of type char
string *str;            //str is a pointer of type string

p = new int;            //allocates memory of type int
                        //and stores the address of the
                        //allocated memory in p
*p = 28;                //stores 28 in the allocated memory

name = new char[5];    //allocates memory for an array of
                        //five components of type char and
                        //stores the base address of the array
                        //in name
strcpy(name, "John");  //stores John in name

str = new string;       //allocates memory of type string
                        //and stores the address of the
                        //allocated memory in str
*str = "Sunny Day";     //stores the string "Sunny Day" in
                        //the memory pointed to by str
```

> 回顾一下，运算符`new`分配特定类型的内存空间，并返回所分配内存空间的地址。然而，如果运算符`new`无法分配所需的内存空间（例如，内存空间不足），那么它会抛出`bad_alloc`异常，如果该异常未被处理，程序将以错误消息终止。异常将在第14章详细讨论。本章还将讨论`bad_alloc`异常。

## 运算符`delete`

假设你有以下声明：

```cpp
int *p;
```

该语句将p声明为int类型的指针变量。接下来，考虑以下语句：

```cpp
p = new int;           //Line 1
*p = 54;               //Line 2
p = new int;           //Line 3
*p = 73;               //Line 4
```

图12-5显示了这些语句的效果。

