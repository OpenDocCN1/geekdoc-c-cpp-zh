
- 成员 `clear` 被调用。

C++ 支持一种*异常*机制来处理异常情况。根据 ANSI/ISO 标准，异常可与流对象一起使用。第10章讨论异常。将异常与流对象一起使用在第10.7节讨论。

## 6.3.2 格式化输出和输入

信息写入流（或偶尔从流中读取）的方式由*格式化标志*控制。

当需要设置输出字段或输入缓冲区的宽度，以及确定值显示的形式（例如*基数*）时，就会使用格式化。大多数格式化特性属于 `ios` 类的范畴。格式化由 `ios` 类定义的标志控制。这些标志可以通过两种方式操作：使用专门的成员函数，或使用*操纵符*，后者可直接插入流或从流中提取。使用任一方法都没有特别理由；通常两种方法都可行。在下面的概述中，首先介绍各种成员函数。随后介绍标志和操纵符本身。提供示例说明如何操作标志以及它们的效果。

许多操纵符无参数，一旦包含流头文件（例如 `iostream`）即可使用。一些操纵符需要参数。要使用后一类操纵符，必须包含头文件 `iomanip`。

### 6.3.2.1 修改格式的成员函数

有几个*成员函数*可用于操作 I/O 格式化标志。除了使用下面列出的成员外，通常还可使用*操纵符*，它们可直接插入流或从流中提取。可用成员按字母顺序列出，但实践中最重要的成员是 `setf`、`unsetf` 和 `width`。

- `ios &ios::copyfmt(ios &obj):` 将 `obj` 的所有格式标志复制到当前 `ios` 对象。返回当前 `ios` 对象。

- `ios::fill() const:` 返回当前填充字符。默认情况下，这是空白字符。

- `ios::fill(char padding):` 重新定义填充字符，并返回*前一个*填充字符。除了使用此成员函数，还可以将 `setfill` *操纵符*直接插入 `ostream`。例如：

  ```cpp
  cout.fill('0');        // use '0' as padding char
  cout << setfill('+');  // use '+' as padding char
  ```

- `ios::fmtflags ios::flags() const:` 返回控制调用该成员函数的流的格式状态的当前标志集。要检查某个特定标志是否已设置，请使用 `bit_and` 运算符。例如：

  ```cpp
  if (cout.flags() & ios::hex)
      cout << "Integral values are printed as hex numbers\n";
  ```

- `ios::fmtflags ios::flags(ios::fmtflags flagset);` 返回*前一组*标志，并由 `flagset` 定义新的标志集。使用 bitor 运算符指定多个标志。例如：

  ```cpp
  // change the representation to hexadecimal
  cout.flags(ios::hex | cout.flags() & ~ios::dec);
  ```

- `int ios::precision() const;` 返回输出浮点值时使用的有效数字位数（默认值：6）。

- `int ios::precision(int signif);` 将输出实数值时使用的有效数字位数设置为 `signif`。返回先前使用的有效数字位数。如果所需位数超过 `signif`，则该数字以“科学”记数法显示（参见[6.3.2.2](#)节）。操纵符：`setprecision`。例如：

  ```cpp
  cout.precision(3);             // 3 digits precision
  cout << setprecision(3);       // same, using the manipulator

  cout << 1.23 << " " << 12.3 << " " << 123.12 << " " << 1234.3 << '\n';
  // displays: 1.23 12.3 123 1.23e+03
  ```

- `ios::fmtflags ios::setf(ios::fmtflags flags);` 设置一个或多个格式化标志（使用 bitor 运算符组合多个标志）。已设置的标志不受影响。返回*前一组*标志。除了使用此成员函数，还可以使用操纵符 `setiosflags`。示例在下一节（[6.3.2.2](#)）中提供。

- `ios::fmtflags ios::setf(ios::fmtflags flags, ios::fmtflags mask);` 清除 mask 中提到的所有标志，并设置 `flags` 中指定的标志。返回*前一组*标志。一些示例如下（但更详细的讨论参见下一节（[6.3.2.2](#)））：

  ```cpp
  // left-adjust information in wide fields
  cout.setf(ios::left, ios::adjustfield);
  // display integral values as hexadecimal numbers
  cout.setf(ios::hex, ios::basefield);
  // display floating point values in scientific notation
  cout.setf(ios::scientific, ios::floatfield);
  ```

- `ios::fmtflags ios::unsetf(ios::fmtflags flags);` 清除指定的格式化标志（其余标志保持不变），并返回*前一组*标志。取消设置活动的默认标志（例如 `cout.unsetf(ios::dec)`）的请求会被忽略。除了此成员函数，也可以使用操纵符 `resetiosflags`。例如：

  ```cpp
  cout << 12.24;                    // displays  12.24
  cout.setf(ios::fixed);
  cout << 12.24;                    // displays  12.240000
  cout.unsetf(ios::fixed);          // undo a previous ios::fixed setting.
  cout << 12.24;                    // displays  12.24
  cout << resetiosflags(ios::fixed); // using manipulator rather
                                     // than unsetf
  ```

- `int ios::width() const;` 返回下一次插入时要使用的当前活动输出字段宽度。默认值为 0，表示“写入该值所需字符数”。

- `int ios::width(int nchars);` 将下一次插入操作的字段宽度设置为 `nchars`，并返回先前使用的字段宽度。此设置不是持久的。每次插入操作后都会重置为 0。操纵符：`std::setw(int)`。例如：

  ```cpp
  cout.width(5);
  cout << 12;                 // using 5 chars field width
  cout << setw(12) << "hello";  // using 12 chars field width
  ```

### 6.3.2.2 格式化标志

大多数格式化标志与输出信息有关。信息基本上可以通过两种方式写入输出流：使用二进制输出，信息直接写入输出流，而不先转换为某种人类可读格式；以及使用格式化输出，首先将存储在计算机内存中的值转换为人类可读文本。格式化标志用于定义这种转换发生的方式。本节涵盖所有格式化标志。格式化标志可以使用成员函数来设置（取消设置），但通常也可以使用具有相同效果的操纵符。对于每个标志，都会展示如何通过成员函数或（如果可用）操纵符来控制它们。

**在宽字段中显示信息：**

- `ios::internal:` 在负数的负号与值本身之间添加填充字符（默认为空格）。其他值和数据类型右对齐。操纵符：`std::internal`。例如：

  ```cpp
  cout.setf(ios::internal, ios::adjustfield);
  cout << internal;        // same, using the manipulator

  cout << '|' << setw(5) << 5 << "\n";  // displays '    5'
  ```

- `ios::left:` 在比显示值所需更宽的字段中左对齐值。操纵符：`std::left`。例如：

  ```cpp
  cout.setf(ios::left, ios::adjustfield);
  cout << left;             // same, using the manipulator

  cout << '|' << setw(5) << "hi" << "\n";  // displays 'hi   '
  ```

- `ios::right:` 在比显示值所需更宽的字段中右对齐值。操纵符：`std::right`。这是默认值。例如：

  ```cpp
  cout.setf(ios::right, ios::adjustfield);
  cout << right;            // same, using the manipulator

  cout << '|' << setw(5) << "hi" << "\n";  // displays '  hi'
  ```

**使用各种数字表示：**

- `ios::dec:` 将整数值显示为十进制数。操纵符：`std::dec`。这是默认值。例如：

  ```cpp
  cout.setf(ios::dec, ios::basefield);
  cout << dec;             // same, using the manipulator
  cout << 0x10;            // displays 16
  ```

