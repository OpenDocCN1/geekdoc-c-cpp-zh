
```
cout << showbase
    << oct << i << endl
    << dec << i << endl
    << hex << i << endl;
```

# 输出

```
032
26
0x1A
```

将由这些语句产生，因为 32₈ = 26₁₀ = 1A₁₆。

下表列出了 iostream 提供的格式操纵符。这些操纵符及其他操纵符将在第 11 章中详细说明。

| 格式操纵符 | 描述 |
|---|---|
| fixed | 对实数值使用定点表示法 |
| scientific | 对实数值使用科学计数法 |
| showpoint | 为整数形式的实数显示小数点及尾随零 |
| noshowpoint | 为整数形式的实数隐藏小数点及尾随零 |
| dec | 对整数输入或输出使用十进制表示法 |
| hex | 对整数输入或输出使用十六进制表示法 |
| oct | 对整数输入或输出使用八进制表示法 |
| showbase | 显示整数值时标明其进制（例如十六进制为 0x） |
| noshowbase | 显示整数值时不标明其进制 |
| showpos | 为正值显示 + 号 |
| noshowpos | 不为正值显示 + 号 |
| boolalpha | 将 bool 值读取或显示为 true 或 false |
| noboolalpha | 不将 bool 值读取或显示为 true 或 false |
| uppercase | 在科学计数法中使用 E；在十六进制中使用 A-F 字符 |
| nouppercase | 在科学计数法中使用 e；在十六进制中使用 a-f 字符 |
| flush | 将流内容写入屏幕（或文件） |
| endl | 向输出流插入换行符并刷新该流 |
| left | 左对齐显示的值，在右侧用填充字符填充 |
| right | 右对齐显示的值，在左侧用填充字符填充 |
| internal | 在符号或进制前缀与数值之间用填充字符填充 |
| skipws | 输入时跳过空白字符 |
| noskipws | 输入时不跳过空白字符 |

有些格式操纵符需要参数，要使用它们，必须包含 iomanip 库。例如，在示例 4.2 的程序中，我们希望指定显示实数值时使用的小数位数（即精度），因此使用了 iomanip 中提供的 setprecision(n) 操纵符，其中 n = 2，将后续实数的小数位精度设置为 2。

另一种格式与显示数据值所用的空间或字段有关。输出字段的默认宽度为 0，会自动增大以适应所显示的值，这通常正是程序员想要的。在需要更宽字段的情况下，我们可以使用 setw(n) 操纵符，它将下一个字段的宽度设置为 n。不过，后续输出的字段宽度会自动恢复为零，因此对于每个要覆盖默认输出格式的值，都必须使用 setw()。

为了说明 setw() 的用法，假设我们正在为构建一台设备所用到的物料创建一份支出报告。如果我们使用如下输出语句：

```
cout << showpoint << fixed
    << "Electrical:    $" << elecCost<< endl
    << "Sheet metal:   $" << metalCost << endl
    << "Wages:         $" << wages << endl
    << "Miscellaneous: $" << miscCost << endl;
```

可能产生的输出如下：

```
Electrical:    $ 1013.
Sheet metal:   $  549.2297
Wages:         $  728.5
Miscellaneous: $   25.
```

如果将金额四舍五入到两位小数并右对齐，看起来会好得多。一种方法是使用 setprecision()、setw() 和 right 操纵符，如下所示：

```
cout << showpoint << fixed
    << setprecision(2) << right
    << "Electrical:    $" << setw(7) << elecCost<< endl
    << "Sheet metal:   $" << setw(7) << metalCost << endl
    << "Wages:         $" << setw(7) << wages << endl
    << "Miscellaneous: $" << setw(7) << miscCost << endl;
```

这将生成如下格式的输出：

```
Electrical:    $ 1013.00
Sheet metal:   $  549.23
Wages:         $  728.50
Miscellaneous: $   25.00
```

用于填充字段空白部分的字符称为填充字符。如前一个示例所示，它默认为空格，但我们可以通过 setfill(ch) 操纵符将其改为另一个字符 ch。例如，如果我们将前面的输出语句改为：

```
cout << showpoint << fixed
    << setprecision(2) << right
    << setfill('*')
    << "Electrical:    $" << setw(7) << elecCost<< endl
    << "Sheet metal:   $" << setw(7) << metalCost << endl
    << "Wages:         $" << setw(7) << wages << endl
    << "Miscellaneous: $" << setw(7) << miscCost << endl;
```

则生成的输出将是：

```
Electrical:    $ 1013.00
Sheet metal:   $ *549.23
Wages:         $ *728.50
Miscellaneous: $ **25.00
```

## 7.4 string 类

7.1 节中的入门示例使用了 C++ 的 string 类来处理 IP 地址。本节将介绍该类的其他一些特性。

### 7.4.1 声明 string 对象

如 7.1 节所示，string 类声明在 string 库中，每个使用它的程序都必须包含该库：

```
#include <string>      // string class
```

因为 string 是一个类的名称，而类的名称是一种类型，所以 string 对象可以像我们学过的其他对象一样进行声明和初始化。例如，声明

```
string address, block1, block2, block3, block4;
```

在示例 7.1 中创建了五个名为 address、block1、block2、block3 和 block4 的 string 对象，并将它们各自初始化为空字符串，空字符串不包含任何字符。空字符串的字面量可以写成两个连续的双引号（""）。

string 对象的声明也可以通过提供字符串表达式作为其初始值来初始化该对象。例如，以下声明

```
string address = "aaa.bbb.ccc.ddd",
    block1 = block2 = block3 = block4 = "";
```

创建 string 对象 address，并将其初始化为包含 15 个字符，

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_243_0.png)

而 `string` 对象 `block1`、`block2`、`block3` 和 `block4` 则各自初始化为空字符串。

这些 string 对象是变量，可以被赋予新值。例如，示例 7.1 中的第一次示例运行会将用于初始化 `address` 的 15 个字符的字符串替换为 18 个字符的字符串。

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_244_0.png)

常量 string 对象通过在一个普通 string 声明前加上关键字 `const` 来定义，例如：

```
const string UNITS = "centimeters";
```

与其他常量一样，这类对象的 `string` 值在程序后续部分不能被更改。

### 7.4.2 string 操作

#### 7.4.2.1 输入、输出与赋值

`string` 类对 `<<`、`>>` 和 `=` 进行了扩展，使其能够在 string 对象上执行这些基本的 I/O 和赋值操作。例如，在大多数程序中，我们使用输出运算符 `<<` 将字符串字面量显示为输入提示，如示例 7.1 所示：

```
cout << "Enter an IP address: ";
```

在同一个程序中，我们使用 `<<` 显示 `string` 变量的值：

```
cout << "The network/host blocks are:\n"
     << block1 << endl << block2 << endl
     << block3 << endl << block4 << endl;
```

赋值运算符 `=` 用于向四个 `string` 变量 `block1`、`block2`、`block3` 和 `block4` 赋值。

此外，当执行以下语句

```
cout << "Enter an IP address: ";
cin >> address;
```

且用户输入 `titan.ksc.nasa.gov` 时，

```
Enter an IP : titan.ksc.nasa.gov
```

字符串 `titan.ksc.nasa.gov` 被赋给了 `address`。但是，如果用户在部分块之间输入了一些空格，

```
Enter an IP address: titan. ksc. nasa.gov
```

字符串 titan. 将被赋给 address，但输入的其余部分会发生什么？

字符串的输入过程与我们介绍的其他类型相同：>> 会跳过前导空白字符，并在下一个空白字符处停止，我们可以将其描述为从输入流中获取下一个“单词”。因此，在前面的例子中，未读的字符 ksc. nasa.gov（包括 ksc 前的空格）会保留在 istream 中，并在后续的输入语句（如果有的话）中被读取。不过，对于示例 7.1 中的程序，执行将终止并出现类似如下的错误消息：

```
Enter an IP address: titan. ksc. nasa.gov
Assertion failed: (dot2 != string::npos), function main, file fig7-1.cpp,
line 28.
```

我们将在本节稍后解释其原因。

string 库确实提供了一个函数 getline()，可以用它将整行文本（包括空白字符）读入一个 string 变量。例如，如果我们将前面的代码片段改写为：

```
cout << "Enter an IP address: ";
getline(cin, address);
```

并输入 titan. ksc. nasa.gov，函数 getline() 将读取整行作为输入，并将其赋值给发送给它的变量 address。程序产生的输出将是：

```
titan
ksc
nasa
gov
```

注意 ksc 和 nasa 前面的前导空格。它们是作为所输入字符串的一部分被读取的，并被赋给了 block2 和 block3。一般来说，更精确地说，getline() 从 istream（例如 cin）中提取字符，并将它们传输到一个 string 变量中，直到遇到换行符；该换行符会从 istream 中移除，但不会存储在 string 变量中。

总之，要读取整行输入，应使用 getline() 函数。若要跳过前导空白字符，然后读取直到下一个空白字符为止的所有字符，则应使用输入运算符 >>。但在同时使用 >> 和 getline() 时必须小心，因为通过 >> 终止字符输入的换行符会留在 istream 中，如果下一条输入语句使用 getline()，它将不会读取任何字符，因为遇到这个换行符会导致它立即终止。
