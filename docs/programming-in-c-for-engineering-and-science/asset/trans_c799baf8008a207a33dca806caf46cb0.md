

characters F, C, or K. 对于数据成员 myDegrees，我们不知道温度可以高到什么程度，但我们将使用绝对零度（0°K，等价于 −273.15°C 和 −459.67°F）作为下界。我们的限制因此是

myScale 将是字符 'F'、'C' 或 'K' 之一

对于 'K'：myDegrees ≥ 0

对于 'C'：myDegrees ≥ −273.15

对于 'F'：myDegrees ≥ −459.67

如果我们在开始时识别并指定此类限制，那么我们就可以以确保它们得到遵守的方式实现各个类操作。

由于这一组条件将在整个类中为真，因此它被称为类不变量。当可以定义此类不变量时，应将其包含在类的文档中，以便用户知道它们是对 Temperature 类型对象的限制。

## 14.3.2 类操作——函数成员

一旦我们决定了类的成员数据并已在私有部分声明它们，我们就可以开始实现类操作了。这是通过添加函数成员，也称为方法来完成的。我们将通过查看一个简单的示例开始研究它们：一个输出方法，用于通过 ostream 显示 Temperature 对象（我们列表中的操作 (vi)）。

### 14.3.2.1 Temperature 输出

正如我们将在本节后面看到的，我们可以扩展输出运算符 << 使其能够用于输出 Temperature 对象，但我们不能简单地将其作为类的函数成员添加。然而，及早拥有一个输出操作是有用的，因为它可以帮助测试其他操作的正确性。

从外部视角来看，输出函数的目的是显示对象数据成员的内容（但可能不是全部）。在我们的例子中，如果我们将函数成员命名为 display()，程序员应该能够编写

```
temp1.display(cout);
```

以将 Temperature 对象 temp1 中的度数和刻度显示到 cout，并编写

```
temp2.display(cerr);
```

以将 temp2 的度数和刻度显示到 cerr。因此，从内部视角来看，对 display() 的调用可以被视为程序发送给你的（一个 Temperature 对象）的消息，以 cout（或 cerr）作为参数——就像有人告诉你

> "嘿你！使用 cout 打印你自己。"

因此，display() 的定义必须提供我（一个 Temperature 对象）应用于我的数据成员以执行该操作的指令。

这种视角导致了对该操作行为的以下规范：

+   接收：out，一个要写入信息的 ostream
+   输出：myDegrees 后跟一个空格然后是 myScale
+   返回：out，其中插入了 myDegrees、一个空格和 myScale

示例 14.2 显示了该方法的定义。由于其简单性，我们使用 inline 指定符在头文件 Temperature.h 中定义它，位于类声明之后。

### 示例 14.2 显示一个 Temperature

```
// ... #includes 和类声明在此

// -------- 输出方法 -----------------------------
inline void Temperature::display(ostream & out) const
{
    out << myDegrees << ' ' << myScale;
}
```

从外部视角来看，向 Temperature 对象发送此消息将显示该对象中存储在数据成员 myDegrees 和 myScale 中的值，因此语句

```
temp1.display(cout);
```

将通过 cout 显示 temp1 的数据成员，而

```
temp2.display(cerr);
```

将通过 cerr 显示 temp2 的数据成员。本节末尾我们将看到如何重载输出运算符（<<）以以通常的方式显示 Temperature 值。

请注意，作为 Temperature 的函数成员之一，display() 必须使用点表示法调用。换句话说，display() 必须作为消息发送给 Temperature 对象。如果我们尝试在不使用点表示法的情况下调用 display()，

```
display(cout); // ERROR!
```

编译器将生成错误，因为我们没有指定接收消息的 Temperature 对象。

> 内联一个函数（参见第 10.6 节）允许编译器用其定义中的代码替换对该函数的调用。将此定义放在头文件中可使此代码对编译器可用。

在此对函数成员定义的首次查看中，我们引入了许多新特性，我们现在将更详细地查看其中的每一个。

### 14.3.2.2 全名

第一个新特性在函数标题中：

```
inline void Temperature::display(ostream & out) const
```

类名通过作用域运算符（::）附加到方法名，以告知编译器它所属的类。由此产生的名称称为函数的全名（或完全限定名）。

在函数成员的定义中使用全名很重要，因为它们可以访问其类的私有成员，但普通函数不能。如果在方法的定义中未使用全名，如

```
inline void display(ostream & out) const // 不是函数成员
{
    out << myDegrees << ' ' << myScale;    // ERROR!
}
```

编译器会将其视为普通（非成员）函数，并且会出现类似

```
Identifier 'myDegrees' is not defined
Identifier 'myScale' is not defined
```

的错误，因为类的私有数据成员对普通的非成员函数不可见。

全名也很重要，因为它们使得不同的类可以拥有同名和相同签名的函数成员。通过使用全名定义每个 display() 方法，编译器可以区分一个定义和另一个定义。

### 14.3.2.3 常量方法

下一个新特性是函数标题末尾的关键字 const：

```
inline void Temperature::display(ostream & out) const
```

这告知编译器 display() 是一个常量方法，这意味着它不得更改 Temperature 类的任何数据成员。任何尝试这样做的行为都将被编译器捕获为错误。将所有不更改类数据成员的函数成员声明为 const 方法是良好的编程实践。

要使方法的定义正确编译，其原型必须存储在类声明的 public 部分内。此外，由于 display() 的原型引用了类型 ostream，我们必须在类声明之前包含 iostream 库：

```
#include <iostream>    // ostream, ...
using namespace std;

class Temperature
{
public:
    void display(ostream & out) const;

private:
    double myDegrees;
    char myScale;
};
```

请注意，对于常量方法，其原型中也必须使用 const 指定符。另请注意，在类本身内部指定 inline 或函数成员的全名并不是必要的。保持这些原型简单可减少类声明中的杂乱，从而提高可读性。出于同样的原因，类的这些方法应记录在单独的文件 Temperature.txt 中。

当然，在数据成员 myDegrees 和 myScale 包含值之前，display() 方法没有任何实际用途。因此，我们将注意力转向可用于初始化这些数据成员的操作。

### 14.3.2.4 构造函数

正如我们所见，一个 Temperature 定义

```
Temperature temp1,
            temp2;
```

将 temp1 和 temp2 定义为可以如下图所示的对象：

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_580_0.png)

问号表示这些对象中的数据成员未定义。某些版本的 C++ 可能会将 myDegrees 初始化为 0 并将 myScale 初始化为空字符 '\0'。在其他版本中，它们的初始值可能是分配给它们的内存位置中位串对应的“垃圾值”；例如，一个版本将 myDegrees 初始化为 -9.3E61，myScale 初始化为不存在的字符，其数字代码为 -52。由于这些垃圾值不代表有效温度，我们当然更希望前面的定义使用我们选择的某个默认值（例如 0 摄氏度）来定义 temp1 和 temp2：

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_580_1.png)

