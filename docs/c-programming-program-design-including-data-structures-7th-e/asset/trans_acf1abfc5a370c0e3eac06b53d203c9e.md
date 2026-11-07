

```cpp
        cout << "Line 7: yourRectangle: "
             << yourRectangle << endl;                //Line 7

        cout << "Line 8: myRectangle + yourRectangle: "
             << myRectangle + yourRectangle << endl;  //Line 8
        cout << "Line 9: myRectangle * yourRectangle: "
             << myRectangle * yourRectangle << endl;  //Line 9

        return 0;
}
```

**示例运行：** 在此示例运行中，用户输入以底纹显示。

```
Line 3: myRectangle: Length = 23; Width = 45
Line 4: Enter the length and width of a rectangle: 32 15

Line 7: yourRectangle: Length = 32; Width = 15
Line 8: myRectangle + yourRectangle: Length = 55; Width = 60
Line 9: myRectangle * yourRectangle: Length = 736; Width = 675
```

第1行和第2行中的语句声明并初始化 myRectangle 和 yourRectangle 为 rectangleType 类型的对象。第3行中的语句使用 cout 和插入运算符输出 myRectangle 的值。第5行中的语句使用 cin 和提取运算符将数据输入到 yourRectangle 中。第7行中的语句使用 cout 和插入运算符输出 yourRectangle 的值。第8行中的 cout 语句将 myRectangle 和 yourRectangle 的长度和宽度相加并输出结果。类似地，第9行中的 cout 语句将 myRectangle 和 yourRectangle 的长度和宽度相乘并输出结果。输出表明，流插入运算符和流提取运算符都已被成功重载。

## 重载赋值运算符（=）

类上的内置操作之一是赋值操作。赋值运算符会导致该类成员变量的逐成员复制。例如，语句：

```cpp
myRectangle = yourRectangle;
```

等价于以下语句：

```cpp
myRectangle.length = yourRectangle.length;
myRectangle.width = yourRectangle.width;
```

回顾第12章可知，内置赋值运算符适用于没有指针成员变量的类，但不适用于有指针成员变量的类。因此，对于有指针成员变量的类，为了避免数据的浅复制，我们必须显式重载赋值运算符。

回顾一下，要为某个类重载赋值运算符 =，运算符函数 operator= 必须是该类的成员。

### 为类重载赋值运算符 = 的通用语法

下面描述为类重载赋值运算符 = 的通用语法。

**函数原型**（需包含在类的定义中）：

```cpp
const className& operator=(const className&);
```

**函数定义：**

```cpp
const className& className::operator=
                         (const className& rightObject)
{
        //local declaration, if any

        if (this != &rightObject)  //avoid self-assignment
        {
                //algorithm to copy rightObject into this object
        }

        //Return the object assigned.
        return *this;
}
```

在函数 operator= 的定义中：

- 只有一个形参。
- 该形参通常是对某个特定类的 const 引用。
- 函数的返回类型是对某个特定类的 const 引用。

现在解释为什么函数 operator= 的返回类型应为类类型的引用。

假设已为类 rectangleType 重载赋值运算符 =。语句：

```cpp
myRectangle = yourRectangle;
```

等价于语句：

```cpp
myRectangle.operator=(yourRectangle);
```

也就是说，对象 yourRectangle 成为函数：

```cpp
operator=
```

的实际参数。

现在考虑语句：

```cpp
myRectangle = yourRectangle = tempRect;
```

由于运算符 = 的结合性是从右到左，该语句等价于语句：

```cpp
myRectangle.operator=(yourRectangle.operator=(tempRect)); //Line A
```

显然，我们必须先执行表达式：

```cpp
yourRectangle.operator=(tempRect)
```

即表达式：

```cpp
yourRectangle = tempRect
```

表达式：

```cpp
yourRectangle.operator=(tempRect)
```

返回的值将成为函数 `operator=` 的参数，以便为对象 myRectangle 赋值（见第 A 行中的语句）。由于函数 `operator=` 的形参是引用参数，表达式：

```cpp
yourRectangle.operator=(tempRect)
```

必须返回对对象的引用，而不是其值。也就是说，它必须返回对对象 yourRectangle 的引用，而不是 yourRectangle 的值。因此，为类重载赋值运算符 = 的函数的返回类型必须是对该类类型的引用。

现在考虑以下语句：

```cpp
myRectangle = myRectangle;                 //Line B
```

这里，我们试图将 myRectangle 的值复制到 myRectangle 中；也就是说，该语句是自赋值。我们必须防止这类赋值的一个原因是它们会浪费计算机时间。不过，首先我们解释赋值运算符的函数体如何防止这类赋值。

如上所述，函数 `operator=` 的函数体确实会防止诸如第 B 行中给出的赋值。我们来看看是如何做到的。

考虑运算符函数 `operator=` 函数体中的 `if` 语句：

```cpp
if (this != &rightObject)   //avoid self-assignment
{
    //algorithm to copy rightObject into this object
}
```

语句：

```cpp
myRectangle = myRectangle;
```

会被编译为语句：

```cpp
myRectangle.operator=(myRectangle);
```

因为函数 `operator=` 由对象 myRectangle 调用，所以函数 `operator=` 函数体中的指针 `this` 指向对象 myRectangle。此外，由于 myRectangle 也是函数 `operator=` 的参数，形参 `rightObject` 也指向对象 `myRectangle`。因此，在表达式：

```cpp
this != &rightObject
```

中，`this` 和 `rightObject` 都表示 `myRectangle` 的地址。因此，该表达式将求值为 `false`，并且 `if` 语句的函数体将被跳过。

> **注意** 本注说明运算符函数的函数体必须防止自赋值的另一个原因。让我们考虑以下类：
>
> ```cpp
> class arrayClass
> {
> public:
>     const arrayClass& operator=(const arrayClass&);
>     .
>     .
>     .
> private:
>     int * list;
>     int length;
>     int maxSize;
> };
> ```
>
> 类 `arrayClass` 有一个指针成员变量 `list`，用于创建存储整数的数组。假设为类 `arrayClass` 重载赋值运算符的函数的定义在没有 `if` 语句的情况下编写，如下所示：
>
> ```cpp
> const arrayClass& arrayClass::operator=
>                          (const arrayClass& otherList)
> {
>     delete [] list;                         //Line 1
>     maxSize = otherList.maxSize;            //Line 2
>     length = otherList.length;              //Line 3
>
>     list = new int[maxSize];                 //Line 4
>
>     for (int i = 0; i < length; i++)         //Line 5
>         list[i] = otherList.list[i];        //Line 6
>
>     return *this;                            //Line 7
> }
> ```
>
> 假设在用户程序中有以下声明：
>
> ```cpp
> arrayClass myList;
> ```
>
> 考虑以下语句：
>
> ```cpp
> myList = myList;
> ```

```cpp
void print() const;
//Function to print the list

void insertEnd(int item);
//Function to insert an item at the end of the list
//Postcondition: if the list is not full,
//              length++; list[length] = item;
//              if the list is full,
//              output an appropriate message

void destroyList();
//Function to destroy the list
//Postcondition: length = 0; maxSize = 0; list = NULL;

cAssignmentOpOverload(int size = 0);
//Constructor
//Postcondition: length = 0; maxSize = size;
//              list is an array of size maxSize

private:
    int maxSize;
    int length;
    int *list;
};
```

类 cAssignmentOpOverload 的成员函数的定义如下：

```cpp
void cAssignmentOpOverload::print() const
{
    if (length == 0)
        cout << "The list is empty." << endl;
    else
    {
        for (int i = 0; i < length; i++)
            cout << list[i] << " ";
        cout << endl;
    }
}

void cAssignmentOpOverload::insertEnd(int item)
{
    if (length == maxSize)
        cout << "List is full" << endl;
    else
        list[length++] = item;
}

void cAssignmentOpOverload::destroyList()
{
    delete [] list;
    list = nullptr;
    length = 0;
    maxSize = 0;
}
```

