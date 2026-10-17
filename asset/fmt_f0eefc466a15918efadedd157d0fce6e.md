
`c:\examplech2_syntax_errors.cpp(11)`: error C2065: `'tempNum'`:

declared identifier

`c:\examplech2_syntax_errors.cpp(13)`: error C2065: `'tempNum'`:

declared identifier

`c:\examplech2_syntax_errors.cpp(13)`: error C2563: mismatch in

formal parameter list

`c:\examplech2_syntax_errors.cpp(13)`: error C2568: `'<<'`: unable to

resolve function overload

`c:\examplech2_syntax_errors.cpp(13)`: note: could be

`std::basic_ostream<Elem, Traits>`

&`std::endl(std::basic_ostream<Elem, Traits>&&)` 

`c:\examplech2_syntax_errors.cpp(15)`: error C2561: `'main'`: function

must return a value

`c:\examplech2_syntax_errors.cpp(5)`: note: see declaration of `'main'`

```
最好以自上下的方式纠正错误，因为第一个错误可能会误导编译器，导致它标记出多个随后的错误，而实际上早之前的某行只出现了一个错误。因此，让我们考虑以下错误：
```

```
c:\examplech2_syntax_errors.cpp(9): error C2146: syntax error:
';' before identifier 'num'
```

表达式 `examplech2_syntax_errors.cpp(9)` 表示第 9 行存在错误。该错误的其余部分指定在标识符 `num` 之前缺少一个 `;`。如果我们查看第 7 行，会发现 `int num` 语句末尾缺少一个分号。因此，我们必须在第 7 行语句的末尾插入 `;`。

接下来，考虑第二个错误：

```
c:\examplech2_syntax_errors.cpp(11): error C2065: 'tempNum': undeclared identifier
```

此错误发生在第 11 行，它指出标识符 `tempNum` 未声明。当我们查看代码时，发现该标识符尚未被声明。我们应该将 `tempNum` 声明为 `int` 类型的变量。

错误：

```
c:\examplech2_syntax_errors.cpp(13): error C2065: 'tempNum': undeclared identifier
```

发生在第 13 行，指定标识符 `tempNum` 未声明。与之前的错误一样，我们必须声明 `tempNum`。注意，一旦我们声明了 `tempNum` 并重新编译，这个之前的错误就会消失。

下一个错误是：

```
c:\examplech2_syntax_errors.cpp(13): error C2563: mismatch in
parameter list
```

此错误发生在第 13 行，表示某些形式参数列表不匹配。对于初学者来说，这个错误有点难以理解。（在第 13 章中，我们将解释运算符 `<<` 的形式参数列表）。然而，随着练习，你将学会如何解释和纠正语法错误。

## 第 2 章：C++ 的基本元素

当程序编译时，你最可能会遇到语法错误。某个位置的语法错误可能会导致后续几条语句出现语法错误。漏掉一个字符导致四或五条错误信息是非常常见的现象。然而，当删除了第一个错误并重新编译程序时，由该错误引起的后续语法错误可能会消失。因此，你应该按照编译器列出的顺序来修正语法错误。随着你对 C++ 越来越熟悉和丰富，你将学会如何快速发现并修复语法错误。此外，编译器不仅能发现语法错误，还会提示甚至直接告诉你错误所在以及如何修复它们。

### 空格的使用

在 C++ 中，当输入数据时，你使用一个或多个空白来分隔数字。空白也用于分隔保留字与标识符，以及它们与其他符号之间。空白绝不能出现在保留字或标识符内部。

### 分号、括号和逗号的使用

所有 C++ 语句都必须以分号结尾。分号也被称为终止符（terminator）。

注意，大括号 `{` 和 `}` 本身并不是 C++ 语句，尽管它们经常出现在没有其他代码的行中。不要将括号视为分隔符，因为它们封装了函数体并与程序的其他部分隔离开。括号还有其他用途，将在第 4 章中解释。

记住，逗号用于分隔列表中的项。例如，当在一个数据类型后声明多个变量时，你就会使用逗号。

### 语义

赋予语言意义的规则集合被称为语义（semantics）。例如，算术运算符的优先级规则就是语义规则。

如果程序包含语法错误，编译器会警告你。那么当程序包含语义错误时会发生什么？你有可能消除程序中的所有错误但程序仍然可以运行。而且如果它运行了，它可能不会按照你的预期执行操作。例如，以下两行代码在语法上都是正确的表达式，但它们的含义不同：

```
2 + 3 * 5
```

以及：

```
(2 + 3) * 5
```

如果你在程序用其中一行代码替换另一行，你将无法得到相同的结果——尽管数字相同，但语义是不同的。你将在书中不断学习语义知识。

### 标识符的命名

考虑以下两组语句：

```
const double A = 2.54; // 转换常量
double x; // 存储厘米的变量
double y; // 存储英寸的变量
```

```
x = y * A;
```

以及

```
const double CENTIMETERS_PER_INCH = 2.54;
double centimeters;
double inches;
```

```
centimeters = inches * CENTIMETERS_PER_INCH;
```

第二组语句中的标识符（如 `CENTIMETERS_PER_INCH`）通常被称为自文档标识符（self-documenting identifiers）。正如你所见，自文档标识符可以使注释变得不必要。

考虑自文档标识符 `annualsale`。这个标识符被称为连续单词（run-through word）。在使用自文档标识符时，可能会无意中包含连续单词，这可能会降低文档的清晰度。你可以通过将每个单词的首字母大写或在新单词之前插入下划线来使连续单词更容易理解。例如，你可以使用 `annualSale` 或 `annual_sale` 来创建一个更清晰的标识符。

在本章前面的部分，我们规定了常量和变量命名的通用规则。例如，用于命名命名常量的标识符全大写。如果该标识符是连续单词，单词之间用下划线字符分隔，例如 `CENTIMETERS_PER_INCH`。

### 提示行

良好文档的一部分是使用编写清晰的提示（prompts），以便用户在与程序交互时知道该做什么。没有什么比坐在正在运行的程序前，却不知道该输入什么或该输入什么更令人沮丧的了。提示行是告知用户该做什么的可执行语句。例如，考虑以下 C++ 语句，它们用于命名一个 `int` 类型的变量：

```
cout << "Enter an integer between 1 and 10 and "
 << "press the return key" << endl;
cin >> num;
```

当这两条语句按照给定的顺序执行时，第一个输出会导致屏幕上出现以下行文本：

Please enter an integer between 1 and 10 and press the return key

看到这一行后，用户就知道他们必须输入一个整数并按回车键。如果程序只包含第二条语句，用户将不知道他们必须输入整数，而计算机将等待输入。前面的输出语句就是提示行的示例。

在程序中，每当需要用户输入时，你必须包含必要的提示行。此外，这些提示行应该包含尽可能多关于可输入的信息。例如，提示行不仅告诉用户输入一个数字，还告知用户数字应该在 1 到 10 之间。

### 文档

你编写程序不仅对你来说清晰的，对其他人也是如此。因此，你必须对你的程序进行适当记录。一个文档良好的程序更容易理解和修改，即使在你最初编写它很久之后也是如此。使用注释对程序进行记录。注释应该出现在程序中以解释其。

### 格式与样式

你编写程序不仅对你来说应该是的，对其他人也是如此。因此，你必须对你的程序进行适当记录。一个文档良好的程序更容易理解和修改，即使在你最初编写它很久之后也是如此。使用注释对程序进行记录。注释应该出现在程序中以解释其。你可能认为 C++ 的规则太多。然而，这些规则赋予了 C++ 极大的自由。例如，考虑以下两种声明方式：

```
int feet;
double x;
```

以及：

```
int feet; double x;
```

这两者的含义相同。然而，第一种更容易阅读。

### 示例 2-30

考虑以下内容：

```
//一个格式化良好的 C++ 程序。
#include <iostream>
#include <string>
using namespace std;
int main(){
    int num;
    double height;
    string name;
    cout << "Enter an integer: ";
    cin >> num;
    cout << endl;
    cout << "num: " << num << endl;
    cout << "Enter the first name: ";
    cin >> name;
    cout << endl;
    cout << "Enter the height: ";
    cin >> height;
    cout << endl;
    cout << "Name: " << name << endl;
    cout << "Height: " << height << endl;
    return 0;
}
```

### 赋值语句的更多

你目前看到的赋值语句被称为简单赋值语句。在某些情况下，你可以使用特殊的复合赋值语句（compound assignment statements）以更简洁的符号来编写简单赋值语句。

对应五个算术运算符 `+`, `-`, `*`, `/` 和 `%`，C++ 提供了相应的复合赋值运算符：`+=`, `-=`, `*=`, `/=` 和 `%=`. 考虑以下简单赋值语句，其中 `x` 和 `y` 是 `int` 变量：

```
x = x * y;
```

使用复合运算符 `*=`, 该语句可以写为：

```
x *= y;
```

一般来说，使用复合运算符 `*=`, 你可以重写简单赋值语句：

```
variable = variable * (expression);
```

为：

```
variable *= expression;
```

其他的算术复合运算符具有类似的约定。例如，使用复合运算符 `+=`, 你可以将简单的赋值语句重写：

```
variable = variable + (expression);
```

重写为：

```
variable += expression;
```

复合赋值语句允许你通过将算术运算符与赋值运算符结合，以简洁的方式编写简单的赋值语句。

### 示例 2-31

此示例展示了几个等同于简单赋值语句的复合赋值语句。

#### 赋值语句

#### 复合赋值语句

```
x = x + 5; 
counter = counter + 1;
sum = sum + number;
amount = amount * (interest + 1);
x = x / (y + 5);
```

```
x += 5;
counter += 1;
sum += number;
amount *= interest + 1;
x /= y + 5;
```

> 任何复合赋值语句都可以转换为简单赋值语句。然而，简单赋值语句可能无法（容易）转换为复合赋值语句。例如，考虑以下简单赋值语句：

```
x = x * y + z - 5;
```

要将此语句写为复合赋值语句，变量 `x` 必须是右侧的公因子，但事实并非如此。因此，你不能立即将此语句转换为复合赋值语句。事实上，等效的复合赋值语句是：

```
x *= y + (z - 5) / x;
```

这比简单赋值语句复杂。此外，在前面的复合语句中，`x` 不能为 0。我们建议避免此类复合表达式。

### 编程示例：转换长度

![](img/d998292a174f7bfd8a26bfbada3d454e_143_0.png)

编写一个程序，以英尺和英寸表示给定长度作为输入。程序随后转换并输出以厘米为单位的长度。假设给定的英尺和英寸为整数。

输入英尺和英寸长度。

输出对应的厘米长度。

长度以英尺和英寸给出，你需要找到对应的厘米。1英寸等于 2.54 厘米。程序需要执行的第一件事是将给定的英尺和英寸转换为总英寸。然后，你可以使用转换公式 1 英寸 = 2.54 厘米来找到对应的厘米长度。要从英尺和英寸转换长度，你需要将英尺数乘以 12（等于 12 英寸），加上给定的英寸。

例如，假设输入是 5 英尺 7 英寸。你按如下方式找到总英寸：

```
totalInches = (12 * feet) + inches
= 12 * 5 + 7
= 67
```

然后你可以应用转换公式 1 英寸 = 2.54 厘米来找到厘米厘米长度：

```
centimeters = totalInches * 2.54
= 67 * 2.54
= 170.1
```

根据对该问题的分析，你可以设计如下算法：

- 1. 获取英尺和英寸的长度。
- 2. 将长度转换为总英寸。
- 3. 将总英寸转换为厘米。
- 4. 输出厘米。

程序的输入是两个数字：一个表示英尺，一个表示英寸。因此，你需要两个变量：一个存储英尺，另一个存储英寸。因为程序将首先将给定的长度转换为英寸，你还需要另一个变量来存储总英寸。你还需要一个变量来存储对应的厘米长度。总之，你需要以下变量：

```
int feet; // 存储给定英尺的变量
int inches; // 存储给定英寸的变量
int totalInches; // 存储总英寸的变量
double centimeters; // 存储厘米长度的变量
```

编程示例：转换长度 | 95

命名常量：为了计算对应的厘米长度，你需要将总数乘以 2.54。与其在程序中直接使用值 2.54，不如你将此值声明为命名常量。同样，为了找到总英寸，你需要将英尺乘以 12 并加上英寸。与其在程序中直接使用 12，你也将把此值声明为命名常量。使用命名常量使得日以后修改程序更加容易。

```
const double CENTIMETERS_PER_INCH = 2.54;
const int INCHES_PER_FOOT = 12;
```

主算法：在前面的章节中，我们分析了问题并确定了计算公式。我们还确定了必要的变量和命名常量。现在我们可以在“问题分析与算法设计”部分扩展算法，以解决此编程示例开头提出的问题。

- 1. 提示用户输入。（如果没有提示行，用户将盯着空白屏幕，不知道该做什么。）
- 2. 获取数据。
- 3. 回显输入。（如果没有这一步，程序执行后用户将不知道输入了什么。）
- 4. 找到英寸。
- 5. 输出英寸。
- 6. 将长度转换为厘米。
- 7. 输出厘米。

```cpp
//头文件
#include <iostream>
using namespace std;
//具名常量
const double CENTIMETERS_PER_INCH = 2.54;
const int INCHES_PER_FOOT = 12;
int main() {
    //声明变量
    int feet, inches;
    int totalInches;
    double centimeters;
    //语句：步骤 1 -  7
    cout << "Enter two integers, one for feet and ";
    cout << "one for inches: ";
    cin << feet >> inches;
    cout << endl;
    cout << "The numbers you entered are " << feet
         << " for feet and " << inches
         << " for inches. " << endl;
    totalInches = INCHES_PER_FOOT * feet + inches;
    cout << "The total number of inches = "
         << totalInches << endl;
    centimeters = CENTIMETERS_PER_INCH * totalInches;
    cout << centimeters << endl;
    return 0;
}
```
