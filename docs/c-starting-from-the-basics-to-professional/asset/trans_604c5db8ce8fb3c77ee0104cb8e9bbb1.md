
零总是回绕到可能的最大整数值。也就是说，对于 32 位无符号 int 类型，-1 会变成 2^32 - 1 或 4294967295，-2 会变成 2^32 - 2 或 4294967294，依此类推。这当然意味着 -10 确实会变成 2^32 - 10，即 4294967286。

**注意** 无符号整数相减的结果回绕成非常大的正数，这种现象有时称为*下溢*。一般来说，下溢是需要注意的情况（我们将在后面的章节中遇到这方面的例子）。自然，相反的现象也存在，称为*溢出*。例如，将 unsigned char 值 253 和 5 相加，不会得到 258——unsigned char 类型变量能容纳的最大值是 255！相反，结果会是 2，即 258 对 256 取模。

**警告** 溢出和下溢的结果只对无符号整数有定义。对于有符号整数类型的变量，超出其类型所能表示的范围时，结果是未定义的——也就是说，它取决于你的编译器及其目标计算机架构。

当赋值右侧的表达式产生的值与左侧变量类型不同时，编译器还会插入隐式转换。下面是一个示例：

```cpp
int y {};
double z {5.0};
y = z;                // Requires an implicit narrowing conversion
```

最后一条语句需要转换赋值右侧表达式的值，以便将其存储为 int 类型。编译器会插入转换来完成这件事，但由于这是窄化转换，它可能会发出警告，提示可能丢失数据。

在编写操作数类型不同的整数运算时要小心。不要依赖隐式类型转换来产生你想要的结果，除非你确定它会这样做。如果你不确定，那么你需要的是显式类型转换，也称为显式强制转换。

## 显式类型转换

要将表达式的值显式转换为给定类型，可以这样写：

```cpp
static_cast<type_to_convert_to>(expression)
```

static_cast 关键字反映了这样的事实：该转换是静态检查的，也就是在代码编译时检查。以后处理类时，你会遇到动态转换，其中转换是动态检查的，也就是在程序执行时检查。转换的作用是将求值 expression 得到的结果转换为尖括号中指定的类型。表达式可以是任何东西，从单个变量到包含大量嵌套括号的复杂表达式。你可以通过如下编写来消除上一节中赋值产生的警告：

```cpp
y = static_cast<int>(z);    // Never a compiler warning this time
```

通过添加显式转换，你向编译器表明窄化转换是有意为之。如果转换不是窄化转换，你很少会添加显式转换。下面是使用 `static_cast<>` 的另一个示例：

```cpp
double value1 {10.9};
double value2 {15.9};
int whole_number {static_cast<int>(value1) + static_cast<int>(value2)};  // 25
```

`whole_number` 的初始化值是 `value1` 和 `value2` 的整数部分之和，因此它们各自被显式转换为 `int` 类型。因此，`whole_number` 的初始值将是 25。注意，与整数除法一样，从浮点类型转换为整数类型使用的是*截断*。也就是说，它只是丢弃浮点数的整个小数部分。

> **提示** `<cmath>` 中的 `std::round()`、`lround()` 和 `llround()` 函数允许你将浮点数舍入到最接近的整数。在许多情况下，这比（隐式或显式）转换所使用的截断更好。

我们前面示例中的转换不会影响存储在 `value1` 和 `value2` 中的值，它们将分别保持为 10.9 和 15.9。转换产生的值 10 和 15 只是临时存储用于计算，然后被丢弃。尽管这两种转换都会造成信息丢失，但当你显式指定转换时，编译器总是假定你知道自己在做什么。当然，如果你这样写，`whole_number` 的值会不同：

```cpp
int whole_number {static_cast<int>(value1 + value2)};  // 26
```

`value1` 和 `value2` 相加的结果将是 26.8，转换为 `int` 类型时结果为 26。这又不同于你改为这样写所得到的结果：

```cpp
int whole_number {static_cast<int>(std::round(value1 + value2))};  // 27
```

与花括号初始化器一贯的情况一样，如果这条语句中没有显式类型转换，编译器将要么拒绝插入隐式窄化转换，要么至少对插入隐式窄化转换发出警告。一般来说，需要显式转换的情况应该很少，尤其是对于基本数据类型。如果你不得不在代码中包含大量显式转换，这通常表明你可以为变量选择更合适的类型。不过，有时确实需要类型转换，所以让我们看一个简单的例子。这个例子将一个以十进制值表示的码制长度转换为码、英尺和英寸：

```cpp
// Ex2_04.cpp
// Using explicit type conversions
import <iostream>;

int main()
{
    const unsigned feet_per_yard {3};
    const unsigned inches_per_foot {12};
    const unsigned inches_per_yard { feet_per_yard * inches_per_foot };

    double length {};
    unsigned int yards {};
    unsigned int feet {};
    unsigned int inches {};

    std::cout << "Enter a length in yards as a decimal: ";
    std::cin >> length;

    // Get the length as yards, feet, and inches
    yards = static_cast<unsigned int>(length);
    feet = static_cast<unsigned int>((length - yards) * feet_per_yard);
    inches = static_cast<unsigned int>(length * inches_per_yard) % inches_per_foot;

    std::cout << length << " yards converts to "
              << yards << " yards "
              << feet << " feet "
              << inches << " inches." << std::endl;
}
```

这是该程序的典型输出：

```text
Enter a length in yards as a decimal: 2.75
2.75 yards converts to 2 yards 2 feet 3 inches.
```

main() 中的前三条语句定义了无符号整数常量，用于在码、英尺和英寸之间进行转换。你将它们声明为常量，以防止它们被意外修改。用于存储将输入转换为码、英尺和英寸结果的变量是 unsigned int 类型，并初始化为零。

从输入值计算整码数的语句如下：

```cpp
yards = static_cast<unsigned int>(length);
```

该转换丢弃 length 值中的小数部分，并将整数结果存储在 yards 中。你可以省略这里的显式转换，让编译器处理，但在这种情况下，写出显式转换总是更好。如果不写，就不能明显看出你意识到了需要转换以及可能的数据丢失。许多编译器还会发出警告。

你用下面这条语句获得整英尺数：

```cpp
feet = static_cast<unsigned int>((length - yards) * feet_per_yard);
```

从 length 中减去 yards，会得到 length 中不足一码的部分，类型为 double。编译器会安排将 yards 中的值转换为 double 类型以进行减法。然后，feet_per_yard 的值会被转换为 double 以进行乘法，最后显式转换将结果从 double 类型转换为 unsigned int 类型。

计算的最后一部分获得剩余的整英寸数：

```cpp
inches = static_cast<unsigned int>(length * inches_per_yard) % inches_per_foot;
```

显式转换作用于 length 中的总英寸数，该总英寸数由 length 与 inches_per_yard 相乘得到。因为 length 是 double 类型，常量值将被隐式转换为 double 类型，以便计算乘积。将 length 中的整数英寸数除以一英尺中的英寸数后得到的余数，就是剩余的英寸数。

### 旧式类型转换

在 `static_cast<>` 于 1998 年左右引入 C++ 之前——所以那是非常非常久以前——显式转换是这样写的：

```cpp
(type_to_convert_to) expression
```

expression 的结果被转换为圆括号之间的类型。例如，前一个示例中计算英寸的语句可以这样写：

```cpp
inches = (unsigned int)(length * inches_per_yard) % inches_per_foot;
```

这种类型转换是 C 语言的遗留物，因此也称为 C 风格类型转换。C++ 中有几种转换现在已被区分开来，但旧式转换语法涵盖了所有这些转换。因此，使用旧式转换的代码更容易出错。你的意图并不总是清楚，而且你可能得不到预期的结果。此外，圆括号与周围的（复合）表达式过于融合——`static_cast<>` 运算符在视觉上要容易发现得多。因此：

> **提示** 你有时仍会看到旧式转换，因为它仍然是语言的一部分，但我们强烈建议你不要在新代码中使用它们。在 C++ 代码中绝不应该再使用 C 风格类型转换。就这样。这也是为什么这会是本书中最后一次提到这种语法……

## 格式化字符串

在本章前面，我们为你编写了一个非常科学的程序，用来为你的新鱼塘推荐合适的直径。对于 20 条平均长度为 9 英寸的鱼，Ex2_03A 产生了以下输出：

```text
Pond diameter required for 20 fish is 8.74039 feet.
```

非常有见地。只不过：我们不知道你怎么想，但每当我们挖池塘时，很少会把尺寸测量到千分之一英寸（使用公制的读者可以理解为百分之一毫米）。大多数鱼真的没那么挑剔。那么，为什么要以如此高的精度输出直径呢？

当然，你可以尝试在将每个数字发送到输出流之前，自己将其舍入到所需的小数位数（实际上，这会是一个有趣的练习）。但肯定有更好的解决方案。我们来探索一下。
