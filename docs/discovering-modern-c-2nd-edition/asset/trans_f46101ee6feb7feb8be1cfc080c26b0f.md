

我们可以通过使用可变引用 `ostream` 作为参数来编写接受各种输出流的输出函数：

```cpp
#include <iostream>
#include <fstream>
#include <sstream>

void write_something(std::ostream& os)
{
    os << "Hi stream, did you know that 3 * 3 = " << 3 * 3 <<
       '\n';
}

int main (int argc, char* argv[])
{
    std::ofstream myfile{"example.txt"};
    std::stringstream mystream;

    write_something(std::cout);
    write_something(myfile);
    write_something(mystream);

    std::cout << "mystream is: " << mystream.str() ; // newline contained
}
```

同样，泛型输入可以使用 `istream` 实现，读写 I/O 可以使用 `iostream` 实现。

## 1.7.5 格式化

=> c++03/formatting.cpp

I/O 流由所谓的 I/O 操作符格式化，它们位于头文件 `<iomanip>` 中。默认情况下，C++ 只打印浮点数的几位数字。因此，我们提高精度：

```cpp
double pi = M_PI;
cout << "pi is " << pi << '\n';
cout << "pi is " << setprecision(16) << pi << '\n';
```

并得到更精确的数字：

```cpp
pi is 3.14159
pi is 3.141592653589793
```

C++20 在第 4.3.1 节中，我们将展示如何将精度调整为类型可表示的位数。与使用宏 `M_PI` 或字面量不同，在 C++20 中我们可以使用 `<numbers>` 中的 `double` 常量 `std::numbers::pi`。

当我们编写表格、向量或矩阵时，需要对齐值以提高可读性。因此，接下来我们设置输出宽度：

```cpp
cout << "pi is " << setw(30) << pi << '\n';
```

结果如下：

```cpp
pi is             3.141592653589793
```

`setw` 仅更改下一次输出，而 `setprecision` 会影响所有后续（数值）输出，与其他操作符一样。提供的宽度被理解为最小值，如果打印的值需要更多空间，我们的表格就会变得难看。

我们还可以要求值左对齐，并用我们选择的字符填充空格，例如 - ：

```cpp
cout << "pi is " << setfill('-') << left
     << setw(30) << pi << '\n';
```

得到：

```cpp
pi is 3.141592653589793----------------
```

另一种格式化方式是直接设置标志。此外，我们强制使用标准化指数表示法中的“科学”计数法：

```cpp
cout.setf(ios_base::showpos);
cout << "pi is " << scientific << pi << '\n';
```

结果为：

```cpp
pi is +3.1415926535897931e+00
```

整数可以用八进制和十六进制表示：

```cpp
cout << "63 octal is " << oct << 63 << ".\n";
cout << "63 hexadecimal is " << hex << 63 << ".\n";
cout << "63 decimal is " << dec << 63 << ".\n";
```

预期输出如下：

```cpp
63 octal is 77.
63 hexadecimal is 3f.
63 decimal is 63.
```

布尔值默认打印为整数 0 和 1。按需，我们可以将其表示为 true 和 false：

```cpp
cout << "pi < 3 is " << (pi < 3) << '\n';
cout << "pi < 3 is " << boolalpha << (pi < 3) << '\n';
```

最后，我们可以重置所有更改的格式选项：

```cpp
int old_precision= cout.precision();
cout << setprecision (16)
...
cout.unsetf(ios_base::adjustfield | ios_base::basefield
 | ios_base::floatfield | ios_base::showpos |
ios_base::boolalpha);
cout.precision(old_precision);
```

每个选项由状态变量中的一位表示。要启用多个选项，我们可以使用按位 OR 组合它们的位模式。

## C++20 1.7.6 新格式化

如前一节所示，传统的流格式化需要大量输入。或者，我们可以使用带有 `printf` 函数和格式字符串的 C 风格输出。这允许我们用少量符号声明之前用多个 I/O 操作符编写的内容。

尽管如此，我们不建议使用 `printf`，原因有二：它不能与用户自定义类型一起使用，且不是类型安全的。格式字符串在运行时解析，后续参数通过一种晦涩的宏机制处理。如果参数与格式字符串不匹配，行为是未定义的，并可能导致程序崩溃。例如，字符串作为指针传递，从所指地址开始，字节被读取并作为 `char` 打印，直到在内存中找到二进制 `0`。如果我们意外尝试将 `int` 作为字符串打印，`int` 值会被误解为一个地址，从中应打印一系列 `char`。这将导致要么输出完全无意义的内容，要么（更可能的是）如果地址不可访问则发生内存错误。我们必须承认，最近的编译器会解析格式字符串（在编译时已知时）并警告参数不匹配。

C++20 中的新 `<format>` 库将格式字符串的表达能力与流 I/O 的类型安全性和用户可扩展性相结合，并增加了在输出中重新排序参数的机会。不幸的是，即使在撰写时最新的编译器（GCC 12.0、Clang 13 和 Visual Studio 16.9.6^14）也不支持 `<format>` 库。因此，我们使用了原型库 `<fmt>`，并避免对这将如何转换为最终标准接口进行随意猜测。我们强烈建议您在 `<format>` 可用时尽快自行将这些示例迁移到 `<format>`。语法不同，但原理相同。

14. 然而，我们读到公告称 VS 16.10 将库完整。

与提供正式规范不同，我们将一些来自 **cppreference.com** 的 `printf` 示例移植到新格式中：

```cpp
print("Decimal:\t{} {:06} {} {:0} {:+} {:d}\n",
    1, 2, 3, 0, 4, -1);
print("Hexadecimal:\t{:x} {:x} {:X} {:#x}\n", 5, 10, 10, 6);
print("Octal:\t\t{:o} {:#o} {:#o}\n", 10, 10, 4);
print("Binary:\t\t{:b} {:#b} {:#b}\n", 10, 10, 4);
```

此片段打印：

```cpp
Decimal:    1 2 000003 0 0 +4 -1
Hexadecimal: 5 a A 0x6
Octal:      12 012 04
Binary:     1010 0 b1010 0 b100
```

前两个数字只是在没有提供任何格式信息的情况下打印。当我们使用格式说明符 "{:d}" 请求十进制数字时，会生成相同的输出。第三个数字将（至少）以 6 个字符宽打印，带前导 0。说明符 + 允许我们强制为所有数字打印符号。printf 允许指定数字的无符号输出。当要打印的值为负数时，这会导致错误的大数字。`<format>` 库避免用户声明无符号输出，因为此信息已包含在相应参数的类型中。如果有人想将负值作为大正数打印，他们必须显式转换它。

第二行演示了我们可以以十六进制打印值——对于大于 9 的数字，既可以使用小写也可以使用大写。说明符 "#" 生成十六进制字面量中使用的前缀 "0x"。同样，我们可以将值打印为八进制和二进制，可选地带有相应的字面量前缀。

对于浮点数，我们有更多格式选项：

```cpp
print("Default:\t{} {:g} {:g}\n", 1.5, 1.5, 1e20);
print("Rounding:\t{:f} {:.0f} {:.22f}\n", 1.5, 1.5, 1.3);
print("Padding:\t{:05.2F} {:.2f} {:1.2 f}\n", 1.5, 1.5, 1.5);
print("Scientific:\t{:E} {:e}\n", 1.5, 1.5);
print("Hexadecimal:\t{:a} {:A}\n\n", 1.5, 1.3);
```

然后我们得到：

```cpp
Default:    1.5 1.5 1e+20
Rounding:   1.500000 2 1.3000000000000000000000444089
Padding:    01.50 1.50 1.50
Scientific: 1.500000E+00 1.500000e+00
Hexadecimal: 0x1.8p+0 0X1.4 CCCCCCCCCCCDP+0
```

使用空花括号或仅包含冒号时，我们得到默认输出。这对应于格式说明符 `"{:g}"`，并产生与不带操作符的流相同的输出。小数位数可以在点和格式说明符 `"{:f}"` 之间给出。然后值将四舍五入到该精度。如果请求的数字大于值类型可表示的范围，最后几位数字就不太有意义。点前的数字指定输出的（最小）宽度。与整数一样，我们可以请求前导 `0`。浮点数可以用大写或小写的 `"e"` 以科学计数法打印，以启动指数部分。十六进制输出可用于用完全相同的位初始化另一个程序中的变量。

输出可以重定向到任何其他 `std::ostream`：15

```cpp
print(std::cerr, "System error code = {}\\n", 7);
ofstream error_file("error_file.txt");
print(error_file, "System error code = {}\\n", 7);
```

15. 需要使用 `<fmt>` 库包含 `ostream.h`。

与 `printf` 不同，现在可以重新排序参数：

```cpp
print("I'd rather be {1} than {0}.\\n", "right", "happy");
```

除了按位置引用参数外，我们还可以为它们命名：

```cpp
print("Hello, {name}! The answer is {number}. Goodbye,
{name}.\\n",
arg("name", name), arg("number", number));
```

或者更简洁地：

```cpp
print("Hello, {name}! The answer is {number}. Goodbye,
{name}.\\n",
"name"_a=name, "number"_a=number);
```

