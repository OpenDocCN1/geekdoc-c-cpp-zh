

这意味着 <<₂ 会尝试将 temp2 插入到 <<₁ 返回的任意值中。

由此可以看出，<<₁ 必须返回一个 ostream。而且，它应该就是 <<₁ 将值插入其中的那个 ostream，因此它应当返回其参数 out。

另一个微妙之处与 operator<< 的返回类型有关。我们为什么将其返回类型定义为 ostream &？原因是，当 C++ 函数以通常方式返回一个值时，它实际上是将该值的一个副本返回给函数的调用者，这意味着对于输出语句 cout << temp1 << temp2;，temp1 会被插入到 cout 中，而 temp2 则会被插入到 cout 的一个副本中，其结果无法预知。

为了避免这种复制，C++ 允许函数使用引用返回类型，这实际上“关闭”了复制机制，并返回实际对象。因此，当我们编写 inline ostream & operator<<(ostream & out, const Temperature & theTemp) { theTemp.display(out); return out; } 时，实际上是在告诉编译器：“不要返回 out 的副本，而是返回它所引用的实际 ostream。”

重载输入运算符 >> 与 << 类似。示例 14.13 给出了 operator>>() 的定义。

## 示例 14.13 重载 Temperature 类的运算符 >>

```
// ------- Temperature istream input -----------------------
inline istream & operator>>(istream & in, Temperature & aTemp)
{
aTemp.read(in);
return in;
}
```

注意，与输出运算符不同，输入运算符确实会修改其 Temperature 参数，因此它被声明为引用参数，而不是常量引用参数。

现在，将针对 Temperature 对象的这些新 I/O 操作添加到我们的温度库中后，示例 14.1 中的温度转换程序就可以编译并运行了。尽管肯定还有其他操作可以添加，但就我们的目的而言，我们可以认为这个库已经完整了。

## 14.4 类的其他特性

在本章中，我们讨论了设计和实现类的主要特性。然而，还有很多内容可以探讨，在本节中我们将讨论另外两个特性。一是提供对类数据成员访问的另一种方式，我们将通过在不使用 read() 和 display() 等方法的情况下实现输入和输出操作来说明这一点。另一个是“类包装器”，应将其添加进来，使我们的类适用于可能使用许多不同类的大型项目。

### 14.4.1 友元函数

尽管对类对象的大多数操作都可以实现为函数成员，但有些情况下这是不可能的。例如，我们看到输出运算符 << 和输入运算符 >> 不能定义为 Temperature 的方法，因为它们的左操作数分别是 ostream 和 istream，而不是 Temperature：

```
cout << "Enter a temperature (e.g., 98.6 F): ";
cin >> theTemperature;

cout << "The temperature is " << theTemperature << endl;
```

我们的解决方案是为 operator<< 和 operator>> 定义使用 Temperature 的 display() 和 read() 方法的“普通”函数：

```
inline ostream & operator<<(ostream & out, const Temperature & aTemp)
{
    aTemp.display(out);
    return out;
}
```

```
inline istream & operator>>(istream & in, Temperature & aTemp)
{
    aTemp.read(in);
    return in;
}
```

现在，假设我们希望在不调用 display() 的情况下定义 operator<<——例如，假设我们的 Temperature 类没有 display() 方法。如果 operator<< 试图直接访问其参数 aTemp 的数据成员，

```
inline ostream & operator<<(ostream & out,const Temperature & aTemp)
{
    out << theTemp.myDegrees << ' '   // ERROR!
        << theTemp.myScale;           // ERROR!
    return out;
}
```

编译器将生成如下错误信息：

```
Member 'myDegrees' is private in class 'Temperature'
```

编译器通过不允许该函数访问类的私有数据成员来强制实现信息隐藏机制。

但假设实现某个操作的唯一合理方式是使用一个必须能够访问类的私有数据成员的函数。在这种罕见的情况下，C++ 允许类通过将该函数指定为友元来授予它这种特殊的访问权限。

为了说明这一点，假设我们从 Temperature 类中删除 display() 方法。那么我们可以将 operator<< 定义为：

```
inline ostream & operator<<(ostream & out, const Temperature & aTemp)
{
    out << theTemp.myDegrees << ' '
        << theTemp.myScale;
    return out;
}
```

前提是我们在类内部放置一个 operator<<( ) 的原型，并在其前面加上关键字 friend：

```
class Temperature
{
public:                    // The class interface
    .
    .
    .
    friend ostream & operator<<(ostream& out, const Temperature & aTemp);
    .
    .
    .
private:                   // The hidden details
    double myDegrees;
    char myScale;
};
```

之前会产生编译错误的同一个定义现在可以正确编译了，因为通过将该函数命名为友元，类授予了该函数访问其私有部分的权限。还要注意，operator<<( ) 没有被指定为 const 函数。这是因为 const 只能应用于函数成员，而 operator<<( ) 不是函数成员。

类似地，我们也可以用 operator>>() 的友元版本替换 read() 方法。在这种情况下，引用参数 aTemp 将不是 const 引用参数，而只是引用参数，因为输入操作会修改它。

### 14.4.1.1 友元的使用

实现类操作时很少需要友元机制。正如我们在 Temperature 类中看到的，对类对象的大多数操作都可以定义为函数成员，因此它们不需要友元机制。

当操作的左操作数类型与正在构建的类不同时，就不能使用方法，必须定义普通函数。但即使在这种不常见的情况下，也可以定义一个公共的中介函数（如 display() 或 read()）供该函数调用。友元机制绝对必要的唯一情况是：操作的左操作数类型与正在构建的类不同，并且该操作必须直接访问类的数据成员。

由于友元机制体现的是定义类操作的外部方法（函数从外部操作一个对象），而不是面向对象方法中“我自己能做”的原则，因此友元机制只应在那些确属必要的罕见情况下使用。

### 14.4.2 条件编译与类“包装器”

每当编译存储在文件中的程序时，首先会由一个名为预处理器的特殊程序对其进行检查。预处理器会扫描整个文件，在文件传递给编译器之前进行一些初步分析。例如，预处理器会去除程序中的所有注释，这样编译器就不必花时间去查找并忽略它们。预处理器的另一项任务是处理所有预处理指令，这些指令是以 # 字符开头的行，例如：

```
#include FileName
```

当预处理器遇到该指令时，它会找到名为 FileName 的文件，并将其插入到程序中的该位置。

对于由许多库文件组成的大型项目，通常每个文件都会包含它所需的类声明。这意味着同一个类可能在项目的多个不同位置被声明，这会导致错误，因为 C++ 不允许一个类被声明多次。

然而，如果头文件 <iostream> 被多次包含，则不会导致错误。为什么？因为 <iostream> 的内容被包含在这样一些指令中，这些指令基本上是告诉预处理器：“如果这是你第一次看到这个类，就继续处理该声明。如果你以前见过它，就跳过该声明。”

我们可以用指令将 Temperature 类包裹起来，告诉预处理器对 Temperature 类也执行同样的操作：

```
#ifndef TEMPERATURE
#define TEMPERATURE
class Temperature
{
public:
    // function members

private:
    // data members
};
#endif
```

