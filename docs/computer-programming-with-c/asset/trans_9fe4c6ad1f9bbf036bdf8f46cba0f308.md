

![](img/57c0d966bb33c67a5a188e6bf39e4e02_817_0.png)

**图 14.36** 类的层次结构

如果不小心将 Scientific 类同时作为 Basic 和 Trigonometric 的子类，就会试图通过两条路径在 Scientific 类中继承 Basic 的特性（一次通过 Trigonometric 类，另一次直接通过 Basic 类），从而造成歧义。编译器不允许出现这种歧义，它会生成一个错误，提示 Trigonometric 的子类已经包含了 Basic 的特性，因此不应再将其显式指定为另一个父类，如图 14.37 所示。

```cpp
class Basic
{
/*Functionalities of Basic calculator*/
};
```

```cpp
class Trigonometric: public Basic
{
/*Functionalities of Trigonometric calculator*/
};
```

```cpp
class Scientific: public Trigonometric
{
/*Functionalities of Scientific calculator*/
};
```

这会导致错误，因为编译器会尝试两次继承类 Basic 的功能：一次通过类 Trigonometric，另一次直接通过类 Basic。因此程序的编译将失败，并给出**歧义错误**。

```cpp
class Scientific: public Trigonometric,
public Basic
{
/*Functionalities of Scientific calculator*/
};
```

Scientific 是 Trigonometric 的子类，因此它将继承 Basic 和 Trigonometric 类的功能。这是因为类 Trigonometric 已经是作为类 Basic 的子类创建的。

**图 14.37** 创建 Basic、Trigonometric 和 Scientific 类层次结构的 C++ 语法

以下是图 14.36 所示设计的完整源代码。

```cpp
#include<iostream.h>
#include<math.h>
class Basic
{
    protected:
    double a;
    double b;
    double result;
    private:
    void inputAB()
    {
    cout<<"Enter two numbers"<<endl;
    cin>>a>>b;
    }
    public:
    void add()
    {
    cout<<"***addition****"<<endl;
    inputAB();
    result=a+b;
    displayResult();
    }

cin>>angle;
}
public:
void sine()
{
    cout<<"***sine****"<<endl;
    inputAngle();
    result= sin(angle);
    displayResult();
}
void cosine()
{
    cout<<"***cosine****"<<endl;
    inputAngle();
    result= cos(angle);
    displayResult();
}
void tangent()
{
    cout<<"***tangent****"<<endl;
    inputAngle();
    result= tan(angle);
    displayResult();
}
void printAngleInput()
    {
    cout<<"Value used by last Trigonometric operation="
    <<angle<<endl;
    }
};
class Scientific: public Trigonometric
{
private:
double value;
void inputLogValue()
    {
    cout<<"Enter the value for which log needs to be calculated"
    <<endl;
    cin>>value;
    }
public:
void naturalLog()
{
    cout<<"***Log to the base e****"<<endl;
    inputLogValue();
result= log(value);
displayResult();
}
void logBase10()
{
    cout<<"***Log to the base 10***"<<endl;
    inputLogValue();
    result= log10 (value);
    displayResult();
}
void printLogInput()
{
    cout<<"Value used by last logarithmic operation="<<value<<endl;
}
void main()
{
    Scientific calculator;
    calculator.add();
    calculator.sub();
    calculator.sine();
    calculator.cosine();
    calculator.naturalLog();
    calculator.printAB();
    calculator.printAngleInput();
    calculator.printLogInput();
}
```

`main()` 函数中的第一条语句

```cpp
Scientific calculator;
```

创建了一个名为 calculator 的 Scientific 类对象。由于 calculator 是最底层子类（Scientific）的对象，我们可以访问 Basic 和 Trigonometric 类的所有成员函数，以及 Scientific 自身定义的成员函数。

语句

```cpp
calculator.add();
calculator.sub();
```

使用对象 `calculator` 调用类 Basic 的 `add()` 和 `sub()` 函数，对两个变量 `a` 和 `b` 执行加法和减法。这是可行的，因为子类对象可以访问类层次结构中直到根节点的任何父类中定义的成员。这两个函数在执行所需操作之前，都会从用户那里接收 `a` 和 `b` 的值作为输入。函数 `displayResult()` 显示变量 `result` 的值，该变量始终存储上一次操作的结果。因此，我们在每个函数中都调用了 `displayResult()` 函数，以在计算机屏幕上打印操作结果。所以，当 `add()` 函数调用 `displayResult()` 函数时，它会打印 `a` 和 `b` 相加的结果，因为此时变量 `result` 中保存的是 `a+b` 的值。而当 `sub()` 函数调用 `displayResult()` 函数时，它会打印 `a-b` 的值，该值在执行减法后立即更新到变量 `result` 中。

语句

```cpp
calculator.sine();
calculator.cosine();
```

使用对象 `calculator` 调用类 Trigonometric 中定义的 sine 和 cosine 函数。请注意，用户自定义函数 `sine()` 调用了定义在 `math.h` 中的内置函数 `sin()`，而用户自定义函数 `cosine()` 调用了同样定义在头文件 `math.h` 中的内置函数 `cos()`。

表 14.1 总结了我们在该程序中创建的不同数学函数，以及它们为获得所需结果而调用的内置函数。

最后，我们调用了 `naturalLog()` 函数来计算成员 `value` 中数值的自然对数（以 e 为底）。

```cpp
calculator.naturalLog();
```

函数 `printAB()` 打印类 Basic 中定义的变量 `a` 和 `b` 的最后值。类似地，函数 `printAngleInput()` 和 `printLogInput()` 分别打印类 Trigonometric 和 Scientific 中定义的变量 `angle` 和 `value` 的最后值。

**表 14.1：** 程序中使用的数学函数总结

| 用户自定义函数名 | 所属类 | 从头文件 `math.h` 中使用的内置函数 |
|---|---|---|
| `sine()` | Trigonometric | **`sin()`**：该函数返回作为参数传入的角度的正弦值。函数原型为 `double sin(double);`。语句 `result= sin(angle);` 将传入角度的正弦值返回到变量 `result` 中。 |
| `cosine()` | Trigonometric | **`cos()`**：该函数返回作为参数传入的角度的余弦值。函数原型为 `double cos(double);`。语句 `result= cos(angle);` 将传入角度的余弦值返回到变量 `result` 中。 |
| `tangent()` | Trigonometric | **`tan()`**：该函数返回作为参数传入的角度的正切值。函数原型为 `double tan(double);`。语句 `result = tan(angle);` 将传入角度的正切值返回到变量 `result` 中。 |
| `naturalLog()` | Scientific | **`log()`**：该函数返回作为参数传入的数值的自然对数（以 e 为底）。函数原型为 `double log(double);`。语句 `result = log(value);` 将传入数值的自然对数返回到变量 `result` 中。 |
| `logBase10()` | Scientific | **`log10()`**：该函数返回作为参数传入的数值的以 10 为底的对数。函数原型如下：`double log10(double);`。语句 `result = log10(value);` 将传入数值的以 10 为底的对数返回到变量 `result` 中。 |

## 14.7 解决多重继承中的歧义

使用多个父类和一个子类创建的继承关系称为多重继承，如图 14.38 所示。我们可能会遇到

![](img/57c0d966bb33c67a5a188e6bf39e4e02_823_0.png)

图 14.38 具有歧义成员变量/成员函数名的多重继承

