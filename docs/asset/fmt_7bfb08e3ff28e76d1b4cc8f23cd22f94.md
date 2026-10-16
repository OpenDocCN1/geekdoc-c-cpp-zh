

从而产生一个不可能的温度值。

保持数据成员私有的另一个原因与类的维护有关。随着时间的推移，我们可能希望通过向公共部分添加操作来增强类，但如果可能的话，我们应保持现有操作的声明不变，这样使用该类的程序就不会失败。然而，我们可能希望修改私有部分中的数据成员或向其添加内容。例如，将来我们可能决定将 `myScale` 的类型改为 `string`，以便存储温标的名称而不仅仅是其首字母。或者我们可能会发现添加一些新的数据成员将提高类的某些操作的性能。

#### 14.3.1.3 类不变量

一旦我们封装并隐藏了数据成员，就几乎准备好开始实现类的操作了。然而，在此之前，我们应该确定类的数据成员值可能存在哪些限制。例如，我们可能规定数据成员 `myScale` 的唯一有效值将是字符 `F`、`C` 或 `K`。对于数据成员 `myDegrees`，我们不知道温度可以高到什么程度，但我们将使用绝对零度（0°K，等价于 −273.15°C 和 −459.67°F）作为下界。我们的限制因此是：

- `myScale` 将是字符 `'F'`、`'C'` 或 `'K'` 之一
- 对于 `'K'`：`myDegrees ≥ 0`
- 对于 `'C'`：`myDegrees ≥ −273.15`
- 对于 `'F'`：`myDegrees ≥ −459.67`

如果我们在开始时识别并指定此类限制，那么我们就可以以确保它们得到遵守的方式实现各个类操作。

由于这一组条件将在整个类中为真，因此它被称为类不变量。当可以定义此类不变量时，应将其包含在类的文档中，以便用户知道它们是对 `Temperature` 类型对象的限制。

## 14.3.2 类操作——函数成员

一旦我们决定了类的成员数据并已在私有部分声明它们，我们就可以开始实现类操作了。这是通过添加函数成员，也称为方法来完成的。我们将通过查看一个简单的示例开始研究它们：一个输出方法，用于通过 `ostream` 显示 `Temperature` 对象（我们列表中的操作 (vi)）。

### 14.3.2.1 Temperature 输出

正如我们将在本节后面看到的，我们可以扩展输出运算符 `<<` 使其能够用于输出 `Temperature` 对象，但我们不能简单地将其作为类的函数成员添加。然而，及早拥有一个输出操作是有用的，因为它可以帮助测试其他操作的正确性。

从外部视角来看，输出函数的目的是显示对象数据成员的内容（但可能不是全部）。在我们的例子中，如果我们将函数成员命名为 `display()`，程序员应该能够编写：

```cpp
temp1.display(cout);
```

以将 `Temperature` 对象 `temp1` 中的度数和刻度显示到 `cout`，并编写：

```cpp
temp2.display(cerr);
```

以将 `temp2` 的度数和刻度显示到 `cerr`。因此，从内部视角来看，对 `display()` 的调用可以被视为程序发送给你的（一个 `Temperature` 对象）的消息，以 `cout`（或 `cerr`）作为参数——就像有人告诉你：

> "嘿你！使用 `cout` 打印你自己。"

因此，`display()` 的定义必须提供我（一个 `Temperature` 对象）应用于我的数据成员以执行该操作的指令。

这种视角导致了对该操作行为的以下规范：

- 接收：`out`，一个要写入信息的 `ostream`
- 输出：`myDegrees` 后跟一个空格然后是 `myScale`
- 返回：`out`，其中插入了 `myDegrees`、一个空格和 `myScale`

示例 14.2 显示了该方法的定义。由于其简单性，我们使用 `inline` 指定符在头文件 `Temperature.h` 中定义它，位于类声明之后。

### 示例 14.2 显示一个 Temperature

```cpp
// ... #includes 和类声明在此

// -------- 输出方法 -----------------------------

inline void Temperature::display(ostream & out) const

{

    out << myDegrees << ' ' << myScale;

}
```

从外部视角来看，向 `Temperature` 对象发送此消息将显示该对象中存储在数据成员 `myDegrees` 和 `myScale` 中的值，因此语句：

```cpp
temp1.display(cout);
```

将通过 `cout` 显示 `temp1` 的数据成员，而：

```cpp
temp2.display(cerr);
```

将通过 `cerr` 显示 `temp2` 的数据成员。本节末尾我们将看到如何重载输出运算符（`<<`）以以通常的方式显示 `Temperature` 值。

请注意，作为 `Temperature` 的函数成员之一，`display()` 必须使用点表示法调用。换句话说，`display()` 必须作为消息发送给 `Temperature` 对象。如果我们尝试在不使用点表示法的情况下调用 `display()`：

```cpp
display(cout); // ERROR!
```

编译器将生成错误，因为我们没有指定接收消息的 `Temperature` 对象。

> 内联一个函数（参见第 10.6 节）允许编译器用其定义中的代码替换对该函数的调用。将此定义放在头文件中可使此代码对编译器可用。

在此对函数成员定义的首次查看中，我们引入了许多新特性，我们现在将更详细地查看其中的每一个。

### 14.3.2.2 全名

第一个新特性在函数标题中：

```cpp
inline void Temperature::display(ostream & out) const
```

类名通过作用域运算符（`::`）附加到方法名，以告知编译器它所属的类。由此产生的名称称为函数的全名（或完全限定名）。

在函数成员的定义中使用全名很重要，因为它们可以访问其类的私有成员，但普通函数不能。如果在方法的定义中未使用全名，如：

```cpp
inline void display(ostream & out) const // 不是函数成员

{

    out << myDegrees << ' ' << myScale;    // ERROR!

}
```

编译器会将其视为普通（非成员）函数，并且会出现类似：

```cpp
Identifier 'myDegrees' is not defined

Identifier 'myScale' is not defined
```

的错误，因为类的私有数据成员对普通的非成员函数不可见。

全名也很重要，因为它们使得不同的类可以拥有同名和相同签名的函数成员。通过使用全名定义每个 `display()` 方法，编译器可以区分一个定义和另一个定义。

### 14.3.2.3 常量方法

下一个新特性是函数标题末尾的关键字 `const`：

```cpp
inline void Temperature::display(ostream & out) const
```

这告知编译器 `display()` 是一个常量方法，这意味着它不得更改 `Temperature` 类的任何数据成员。任何尝试这样做的行为都将被编译器捕获为错误。将所有不更改类数据成员的函数成员声明为 `const` 方法是良好的编程实践。

要使方法的定义正确编译，其原型必须存储在类声明的 `public` 部分内。此外，由于 `display()` 的原型引用了类型 `ostream`，我们必须在类声明之前包含 `iostream` 库：

```cpp
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

请注意，对于常量方法，其原型中也必须使用 `const` 指定符。另请注意，在类本身内部指定 `inline` 或函数成员的全名并不是必要的。保持这些原型简单可减少类声明中的杂乱，从而提高可读性。出于同样的原因，类的这些方法应记录在单独的文件 `Temperature.txt` 中。

当然，在数据成员 `myDegrees` 和 `myScale` 包含值之前，`display()` 方法没有任何实际用途。因此，我们将注意力转向可用于初始化这些数据成员的操作。

### 14.3.2.4 构造函数

正如我们所见，一个 `Temperature` 定义：

```cpp
Temperature temp1,

            temp2;
```

将 `temp1` 和 `temp2` 定义为可以如下图所示的对象：

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_580_0.png)

问号表示这些对象中的数据成员未定义。某些版本的 C++ 可能会将 `myDegrees` 初始化为 0 并将 `myScale` 初始化为空字符 `'\0'`。在其他版本中，它们的初始值可能是分配给它们的内存位置中位串对应的“垃圾值”；例如，一个版本将 `myDegrees` 初始化为 -9.3E61，`myScale` 初始化为不存在的字符，其数字代码为 -52。由于这些垃圾值不代表有效温度，我们当然更希望前面的定义使用我们选择的某个默认值（例如 0 摄氏度）来定义 `temp1` 和 `temp2`：

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_580_1.png)

```cpp

inline char Temperature::getScale() const

{

    return myScale;

}

```

由于函数成员的原型必须存储在类声明中，我们将这些访问器的原型添加到我们的类 `Temperature` 中：

```cpp

class Temperature

{

public:

    Temperature();

    Temperature(double initDegrees, char initScale);

    double getDegrees() const;

    char getScale() const;

    void display(ostream & out) const;

private:

    double myDegrees;

    char myScale;

};

```

与常见做法一样，我们已根据用途将这些原型分组，并在每个组之间用空行分隔，如前面的列表所示。例如，构造函数、访问器和 I/O 方法各有不同的用途，因此我们相应地对它们的原型进行分组。

## 14.3.2.7 Temperature Input

接下来，我们为输出函数成员 `display()` 添加一个对应的方法——一个从 `istream` 读取 `Temperature` 值的输入方法。如下语句：

```cpp

temp2.read(cin);

```

应从 `cin` 读取一个数字和一个字符，并分别存储到 `temp2.myDegrees` 和 `temp2.myScale` 中。

与输出操作一样，从内部视角出发，得出以下规范：

- 接收：`in`，一个包含 `double` 和 `char` 的 `istream`
- 输入：`inDegrees`，`double` 值，以及 `inScale`，`char` 值
- 前置条件：`inScale` 为 `{'f', 'c', 'k', 'F', 'C', 'K'}` 之一且 `inDegrees` 对 `inScale` 有效。
- 返回：`in`，其中 `inDegrees` 和 `inScale` 已从中提取
- 后置条件：`myDegrees == inDegrees && myScale == inScale`

为了方便用户，我们将接受大写或小写的刻度并将小写输入转换为大写。为了防止无效输入值，我们必须在修改数据成员之前检查输入的度和刻度是否满足前置条件。如果不满足，我们将终止程序的执行。⁴

由于其复杂性，我们不将此函数成员定义为 `inline`，因此其定义应存储在 `Temperature.cpp` 中，并且由于它修改了 `Temperature` 数据成员，因此未定义为 `const` 方法。示例 14.6 展示了此操作的其中一种实现。

### Example 14.6 Temperature Input

```cpp

// -------- Temperature Input -----------------------------------------

void Temperature::read(istream & in)

{

    double inDegrees;            // temporary variables to

    char inScale;                //   store the input value

    in >> inDegrees >> inScale;  // read values from in

    if (islower(inScale))        // if scale is lowercase

        inScale = toupper(inScale);  //   convert it to uppercase

    //----- Check the class invariant -----

    if (  inScale == 'F' && inDegrees >= MIN_FAHRENHEIT

       || inScale == 'C' && inDegrees >= MIN_CELSIUS

       || inScale == 'K' && inDegrees >= MIN_KELVIN)

    {

        myScale = inScale;        // assign input values

        myDegrees = inDegrees;    //   to data members

    }

    else                        // otherwise issue error message

    {                           // & stop execution

        cerr << "\n*** Invalid temperature *** "

             << initDegrees << ' ' << initScale << endl;

        exit(1);

    }

}

```

作为函数成员，`read()` 的原型必须添加到类声明中：

```cpp

class Temperature

{

public:

    Temperature();

    Temperature(double initDegrees, char initScale);

```

> ⁴ 一种替代方案是使用 `setstate()` 函数设置 `ios::failbit` 以发出输入失败信号，如第 11.3 节所述。然后使用 `Temperature` 类的程序可以用 `failure()` 函数检测此失败并从中恢复。

```cpp

double getDegrees() const;

char getScale() const;

void display(ostream & out) const;

void read(istream & in);

private:

    double myDegrees;

    char   myScale;

};

```

与之前一样，还必须将它的文档添加到文档文件中。

现在程序可以使用 `read()` 从 `istream` 或 `ifstream` 输入温度。

```cpp

Temperature temp1;

...

temp1.read(cin);

...

```

本节后面我们将看到如何重载输入运算符 (`>>`) 以以通常的方式输入 `Temperature` 值。

## 14.3.2.8 Conversion Methods

接下来，我们检查将温度转换为不同刻度的方法。我们首先从函数成员 `toFahrenheit()` 开始。它的规范很简单：

Return: The Fahrenheit temperature equivalent of myself

示例 14.7 给出了此方法的实现。它足够复杂，因此未定义为 `inline`。请注意使用 `switch` 语句根据 `myScale` 的当前值选择适当的转换公式。

### Example 14.7 The `toFahrenheit()` Method

```cpp

// -------- Fahrenheit conversion method ----------------

Temperature Temperature::toFahrenheit() const

{

    switch (myScale)

    {

        case 'F': case 'f':

            return Temperature(myDegrees, 'F');

        case 'C': case 'c':

            return Temperature(myDegrees * 1.8 + 32.0, 'F');

        case 'K': case 'k':

            return Temperature((myDegrees - 273.15) * 1.8 + 32.0, 'F');

    }

}

```

需要注意的是，此函数如何使用显式值 `Temperature` 构造函数来构建要返回的 `Temperature` 值。例如，在 `switch` 语句的第一个 `case` 中，它使用传递给它的 `myDegrees` 和 `'F'` 的值来构建一个 `Temperature` 对象，然后 `toFahrenheit()` 将其用作此 `case` 的返回值。

与往常一样，我们必须将转换方法的原型放在类声明中：

```cpp

