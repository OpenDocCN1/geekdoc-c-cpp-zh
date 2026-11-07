

```cpp
int i;                                      //Line 12
int number;                                  //Line 13

cout << "Line 14: Enter 5 integers: ";      //Line 14

for (i = 0; i < 5; i++)                      //Line 15
{
    cin >> number;                            //Line 16
    intList1.insertEnd(number);               //Line 17
}

cout << endl;                                 //Line 18
cout << "Line 19: intList1: ";               //Line 19
intList1.print();                             //Line 20

intList3 = intList2 = intList1;               //Line 21

cout << "Line 22: intList2: ";               //Line 22
intList2.print();                             //Line 23

intList2.destroyList();                       //Line 24

cout << endl;                                 //Line 25
cout << "Line 26: intList2: ";               //Line 26
intList2.print();                             //Line 27

cout << "Line 28: After destroying intList2, "  //Line 28
     << "intList1: ";                         //Line 29
intList1.print();

cout << "Line 30: After destroying intList2, "  //Line 30
     << "intList3: ";                         //Line 31
intList3.print();
cout << endl;                                  //Line 32

return 0;
```

**示例运行：**在此示例运行中，用户输入以阴影显示。

```
Line 14: Enter 5 integers: 8 5 3 7 2
```

```
Line 19: intList1: 8 5 3 7 2
Line 22: intList2: 8 5 3 7 2

Line 26: intList2: The list is empty.
Line 28: After destroying intList2, intList1: 8 5 3 7 2
Line 30: After destroying intList2, intList3: 8 5 3 7 2
```

第9行的语句创建了大小为10的intList1；第10行和第11行的语句创建了（默认）大小为50的intList2和intList3。第15至17行的语句将数据输入到intList1中，第20行的语句输出intList1。第21行的语句将intList1复制到intList2，然后将intList2复制到intList3。第23行的语句输出intList2（参见示例运行中的第22行，其中包含第22行和第23行的输出）。第24行的语句销毁intList2。第27行的语句输出已为空的intList2（参见示例运行中的第26行，其中包含第26行和第27行的输出）。销毁intList2后，程序输出intList1和intList3的内容（参见示例运行中的第28行和第30行）。示例运行清楚地表明，销毁intList2既不影响intList1，也不影响intList3，因为intList1和intList3各自拥有自己的数据。

## 重载一元运算符

重载一元运算符的过程类似于重载二元运算符的过程。唯一区别在于，对于二元运算符，运算符有两个操作数；对于一元运算符，运算符只有一个参数。因此，要为某个类重载一元运算符：

- 1. 如果运算符函数是类的成员，则它没有参数。
- 2. 如果运算符函数是非成员（即类的`friend`函数），则它有一个参数。

接下来，我们描述如何重载递增和递减运算符。

### 重载递增（++）和递减（--）运算符

递增运算符有两种形式：前置递增（++u）和后置递增（u++），其中u是一个变量，比如`int`类型。对于前置递增++u，变量u的值会在u用于表达式之前先加1。对于后置递增，u的值先用于表达式，然后才加1。

### 重载前置递增运算符。

重载前置递增运算符非常简单。在函数定义中，首先将对象的值加1，然后使用指针`this`返回对象的值。

例如，假设我们为`class` rectangleType重载前置递增运算符，使矩形的长度和宽度都增加1。再假设运算符函数`operator++`是`class` rectangleType的成员。此时运算符函数`operator++`没有参数。由于运算符函数`operator++`没有参数，我们使用指针`this`返回对象增加后的值：

```cpp
rectangleType rectangleType::operator++()
{
    //increment the length and width
    ++length;
    ++width;
    return *this; //return the incremented value of the object
}
```

因为myRectangle是类型为rectangleType的对象，语句：

```cpp
++myRectangle;
```

将myRectangle的长度和宽度都增加1。此外，与myRectangle关联的指针this返回myRectangle增加后的值，该值被忽略。

现在，yourRectangle也是类型为rectangleType的对象，因此语句：

```cpp
yourRectangle = ++myRectangle;
```

将myRectangle的长度和宽度都增加1，与myRectangle关联的指针this返回myRectangle增加后的值，该值被复制到yourRectangle中。

### 将前置递增运算符 ++ 重载为成员函数的一般语法

下面描述将前置递增运算符 ++ 重载为成员函数的一般语法。

**函数原型**（要包含在类的定义中）：

```cpp
className operator++();
```

**函数定义：**

```cpp
className className::operator++()
{
    //increment the value of the object by 1
    return *this;
}
```

重载前置递增运算符的运算符函数也可以是rectangleType类的非成员函数，我们接下来将对此进行描述。

```cpp
rectangleType operator++(rectangleType& rectangle)
{
    //increment the length and width of the rectangle
    (rectangle.length)++;
    (rectangle.width)++;
    return rectangle; //return the incremented
                      //value of the object
}
```

### 将前置递增运算符 ++ 重载为非成员函数的一般语法

下面描述将前置递增运算符 ++ 重载为非成员函数的一般语法。

**函数原型**（要包含在类的定义中）：

```cpp
friend className operator++(className&);
```

**函数定义：**

```cpp
className operator++(className& incObj)
{
    //increment incObj by 1
    return incObj;
}
```

### 重载后置递增运算符

我们现在讨论如何重载后置递增运算符。与前置递增运算符的情况一样，我们首先描述将该运算符重载为类的成员函数。

让我们为**类** `rectangleType`重载后置递增运算符。在前置和后置递增两种情况下，运算符函数的名称相同——`operator++`。为了区分前置和后置递增运算符的重载，我们在运算符函数的函数头中使用一个哑参数（类型为`int`）。因此，**类** `rectangleType`的后置递增运算符的函数原型为：

```cpp
rectangleType operator++(int);
```

语句：

```cpp
myRectangle++;
```

会被编译器编译为如下语句：

```cpp
myRectangle.operator++(0);
```

因此，带参数的函数operator++会被执行。参数0仅用于区分前置和后置递增运算符函数。

后置递增运算符首先在表达式中使用对象的值，然后将对象的值加1。因此，实现此函数所需的步骤如下：

- 1. 将对象的值保存到（例如）temp中。
- 2. 将对象的值加1。
- 3. 返回保存在temp中的值。

**类** `rectangleType`的后置递增运算符的函数定义为：

```cpp
rectangleType rectangleType::operator++(int u)
```

