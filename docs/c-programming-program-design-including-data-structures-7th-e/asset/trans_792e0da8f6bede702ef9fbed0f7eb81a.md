
- b.

```cpp
smartObject.secret();
superSmartObject.z = 0;
```

- c.

```cpp
void superSmart::set(int a, int b, int c)
{
    smart::set(a, b);
    z = c;
}
```

- d. 假设以下语句位于用户程序中：

`smart.print();`

- e. 假设以下语句位于用户程序中：

`cout << superSmart.sum() << superSmart.z << endl;`

- 16. 假设采用习题14的声明。（3, 4）

  - a. 编写 `smart` 的默认构造函数的定义，使 `smart` 的实例变量初始化为0。
  - b. 编写 `superSmart` 的默认构造函数的定义，使 `superSmart` 的实例变量初始化为0。
  - c. 编写 `smart` 的成员函数 `set` 的定义，使实例变量根据参数进行初始化。
  - d. 编写类 `smart` 的成员函数 `sum` 的定义，使其返回实例变量之和。
  - e. 编写类 `superSmart` 的成员函数 `manipulate` 的定义，使其返回 `(x + y)^z`，即返回 x 加 y 的 z 次幂。

- 17. 假设类 `two` 派生自类 `one`。为避免这些类被多次包含，在包含这些类定义的头文件中使用了哪些预处理指令。请举例说明你的答案。（7）

- 18. 
  - a. 类 `ifstream` 派生自哪个类？（7）
  - b. 类 `ofstream` 派生自哪个类？（7）

- 19. 解释在私有继承中，基类的成员如何被派生类继承。（8）

- 20. 解释在保护继承中，基类的成员如何被派生类继承。（8）

- 21. 解释在公有继承中，基类的成员如何被派生类继承。（8）

- 22. 解释类的私有成员和保护成员之间的区别。（8）

- 23. 解释类的保护成员和公有成员之间的区别。（8）

- 24. 考虑以下类定义：

```cpp
class first
{
public:
    void setX();
    void print() const;
protected:
    int y;
    void setY(int a);
private:
    int x;
};
```

假设类 second 使用以下语句派生自类 first：

```cpp
class second: private first
```

确定类 first 的哪些成员在类 second 中是私有、保护和公有的。（8）

- 25. 假设采用习题24的声明。假设类 third 使用以下语句派生自类 first：

```cpp
class third: protected first
```

确定类 first 的哪些成员在类 third 中是私有、保护和公有的。（8）

- 26. 假设采用习题24的声明。假设类 fourth 使用以下语句派生自类 first：

```cpp
class fourth: public first
```

确定类 first 的哪些成员在类 fourth 中是私有、保护和公有的。（8）

- 27. 假设采用习题24的声明。假设类 fifth 使用以下语句派生自类 first：

```cpp
class fifth: first
```

确定类 first 的哪些成员在类 fifth 中是私有、保护和公有的。（8）

- 28. 以下代码有什么错误？（8）

```cpp
class classA
{
protected:
    void setX(int a);                 //Line 1
        //Postcondition: x = a;        //Line 2

private:                              //Line 3
    int x;                             //Line 4
};
```

![](img/d0be7fc6d804b63484835c6c8bc67a07_853_0.png)

```cpp
int main()
{
    classA aObject;                 //Line 5

    aObject.setX(4);                //Line 6
    return 0;                       //Line 7
}
```

- 29. 考虑以下代码：（3, 8）

```cpp
class one
{
public:
    void print() const;
        //Output the values of x and y
protected:
    void setData(int u, int v);
        //Postcondition: x = u; y = v;
private:
    int x;
    int y;
};

class two: public one
{
public:
    void setData(int a, int b, int c);
        //Postcondition: x = a; y = b; z = c;
    void print() const;
        //Output the values of x, y, and z
private:
    int z;
};
```

  - a. 编写类 two 的函数 setData 的定义。
  - b. 编写类 two 的函数 print 的定义。

- 30. 以下 C++ 程序的输出是什么？（1, 2, 3, 4, 8）

```cpp
#include <iostream>
#include <string>

using namespace std;

class baseClass
{
public:
    void print() const;

    baseClass(string s = " ", int a = 0);
        //Postcondition: str = s; x = a;

protected:
    int x;

private:
    string str;
};

class derivedClass: public baseClass
{
public:
    void print() const;

    derivedClass(string s = "", int a = 0, int b = 0);
    //Postcondition: str = s; x = a; y = b;

private:
    int y;
};

int main()
{
    baseClass baseObject("This is the base class", 2);
    derivedClass derivedObject("DDDDDD", 3, 7);

    baseObject.print();
    derivedObject.print();

    return 0;
}
void baseClass::print() const
{
    cout << x << " " << str << endl;
}

baseClass::baseClass(string s, int a)
{
    str = s;
    x = a;
}

void derivedClass::print() const
{
    cout << "Derived class: " << y << endl;
    baseClass::print();
}

derivedClass::derivedClass(string s, int a, int b)
                         :baseClass("Hello Base", a + b)
{
    y = b;
}
```

## 编程练习

- 1. 在第10章中，设计了类 `clockType` 来实现程序中的一天中的时间。某些应用除了小时、分钟和秒之外，可能还要求存储时区。通过添加一个用于存储时区的成员变量，从类 `clockType` 派生类 `extClockType`。添加必要的成员函数和构造函数，使该类能够正常工作。同时，编写成员函数和构造函数的定义。最后，编写一个测试程序来测试你的类。

- 2. 在本章中，设计了类 `dateType` 来实现程序中的日期，但成员函数 `setDate` 和构造函数在将日期存储到成员变量之前没有检查日期是否有效。重写函数 `setDate` 和构造函数的定义，以便在将日期存储到成员变量之前检查月、日和年的值。添加一个成员函数 `isLeapYear`，用于检查某一年是否为闰年。此外，编写一个测试程序来测试你的类。

- 3. 第10章定义了类 `circleType` 来实现圆的基本属性。（向该类添加函数 print，以输出圆的半径、面积和周长。）现在每个圆柱都有一个底面和高度，其中底面是一个圆。设计一个类 `cylinderType`，它能够表示圆柱的属性并对圆柱执行常见操作。从第10章设计的类 `circleType` 派生该类。可以对圆柱执行的一些操作如下：计算并打印体积，计算并打印表面积，设置高度，设置底面半径，以及设置底面圆心。此外，编写一个程序来测试对圆柱的各种操作。

- 4. Amanda 和 Tyler 开了一家专门用圆柱形容器运输液体（如牛奶、果汁和水）的企业。运费取决于容器中液体的量。（为简单起见，可以假设容器装到顶部。）他们还提供以合理价格给容器外表面上漆的选项。编写一个程序，完成以下操作：

  - a. 提示用户输入容器的尺寸（以英尺为单位）（底面半径和高度）。
  - b. 提示用户输入每升运费。
  - c. 提示用户输入每平方英尺的油漆成本。（假设包括顶部和底部在内的整个容器都需要上漆。）
  - d. 分别输出运费和油漆成本。你的程序必须使用类 `cylinderType`（在编程练习3中设计）来存储底面半径和容器高度。（注意：1立方英尺 = 28.32升，或1升 = 0.353146667立方英尺。）

